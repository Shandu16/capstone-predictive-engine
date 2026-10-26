# SS3 Part B — STADIOEquities 7-Day Funding Prediction (Random Forest)

Applies the final SS2 method, a **Random Forest classifier**, to the new client extract `stadioequities_client_funding_extract.csv` (28,502 rows, accounts opened Jan 2022 – Aug 2026).
**Target:** `is_funded` — did the client make a first deposit within 7 days of registering?

## Where things are

| Path | What it is |
|---|---|
| `SS3_PartB.ipynb` | The deliverable: executed notebook with the five required components clearly headed. |
| `Datasets/stadioequities_client_funding_extract.csv` | Client extract (synthetic, supplied for CAP182). |
| `Datasets/STADIOEquities_DATA_DICTIONARY.md` | Column descriptions and data-quality notes supplied with the extract. |
| `Models/rf_funding_model.joblib` | Trained Random Forest. |
| `Experimental results/SS3_PartB/` | Figures, `metrics.json`, `classification_report_test.txt`. |

## Notebook components

| Component | Notebook heading | Marks |
|---|---|---|
| Dataset loading, with markdown on instances, classes and imbalance | **1. DATASET LOADING** | 2 |
| Preprocessing, train/validation/test split, with markdown justification | **2. DATASET PREPROCESSING** | 5 |
| Training, with hyper-parameter justification | **3. MODEL TRAINING** | 5 |
| Evaluation on the unseen test set, metrics and robustness checks | **4. MODEL VALIDATION (UNSEEN DATA)** | 5 |
| Training/ROC/PR curves, confusion matrices, feature importance | **5. RESULTS VISUALISATION** | 3 |

## How to run (VS Code)

1. Clone the repository and open its **root folder** in VS Code (`File → Open Folder`), so that `Datasets/`, `Models/` and `Experimental results/` resolve correctly.
2. Install the VS Code **Python** and **Jupyter** extensions.
3. Create and activate a virtual environment, then install the dependencies:
   ```bash
   python -m venv .venv
   .venv\Scripts\activate          # Windows   (macOS/Linux: source .venv/bin/activate)
   pip install -r requirements.txt  # needs pandas, numpy, scikit-learn, joblib, matplotlib, seaborn, jupyter/ipykernel
   ```
4. Open `SS3_PartB.ipynb`, choose the `.venv` interpreter as the kernel (top right), and select **Run All**. The notebook reads `Datasets/stadioequities_client_funding_extract.csv` and writes figures and metrics to `Experimental results/SS3_PartB/` and the trained model to `Models/rf_funding_model.joblib`. All randomness is seeded (`random_state=42`), so results are reproducible.

## Data and preprocessing (summary)
* 28,502 rows → **28,417** after removing 85 exact duplicates. Classes: `No` 19,138 (67.35 %), `Yes` 9,279 (32.65 %), about 2.06 : 1.
* Dropped: `_id`; `first_deposit_ts` and `initial_deposit_zar` (only exist for funded clients, i.e. **target leakage**); `registration_ts` (only the year is extracted, for a drift check).
* Categorical text normalised, blank categories kept as `Unknown`, 18 impossible ages set to missing, then **median-imputed with missing-indicator columns** (Random Forest needs complete inputs) and one-hot encoded. Imputer and encoder are fitted on the training split only.
* Stratified 70 / 15 / 15 train / validation / test split.

## Model
`RandomForestClassifier(n_estimators=500, max_features="sqrt", class_weight="balanced_subsample", oob_score=True)`. `max_depth` ∈ {6, 10, 16, None} and `min_samples_leaf` ∈ {1, 5, 20, 50} were chosen on the validation set (selected: `max_depth=None`, `min_samples_leaf=50`). The decision threshold (0.585) was chosen on validation (max F1) and frozen for the test set. Every choice is justified in the notebook.

## Results (unseen test set, n = 4,263)

| Metric | Train | Validation | **Test** |
|---|---|---|---|
| ROC-AUC | 0.903 | 0.882 | **0.890** |
| PR-AUC | 0.766 | 0.709 | **0.731** |
| Accuracy | 0.800 | 0.802 | **0.796** (majority baseline 0.674) |
| Balanced accuracy | 0.847 | 0.850 | **0.845** |
| F1 (funded) | 0.763 | 0.765 | **0.760** |
| Recall / Precision (funded) | 0.983 / 0.623 | 0.987 / 0.625 | **0.988 / 0.617** |

Out-of-bag AUC 0.886; 5-fold CV ROC-AUC 0.886 ± 0.006.

Key findings:
1. **Mild over-fitting at most.** The train–validation AUC gap is about 0.02, and test performance matches validation.
2. **KYC completion dominates.** Under 1 % of KYC abandoners fund versus about 62 % of completers; without any KYC-stage feature test ROC-AUC falls from about 0.89 to 0.67.
3. **When it says "will not fund" it is right 99.2 % of the time**, but it flags only 70.3 % of true non-funders at this threshold.
4. **No drift in this extract:** training on 2022–2024 and testing on 2025–2026 gives ROC-AUC 0.886.

## Limitations
The data are synthetic. The 7-day funding rate (32.7 %) differs from the 59 % activation rate in the project brief because this target counts only deposits within 7 days. KYC completion is known only at the end of onboarding, so the model scores clients after onboarding rather than predicting abandonment mid-flow.
