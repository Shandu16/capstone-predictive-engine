# Feature Engineering

**Related Script:** `bank_marketing_pipeline.ipynb`

**Techniques Applied:**
1. **One-Hot Encoding:** Categorical variables (e.g., `job`, `marital`, `education`) are transformed into binary matrices using `pd.get_dummies()`.
2. **Class Imbalance Handling (SMOTE):** The dataset is heavily imbalanced toward clients who did not subscribe. SMOTE is applied to the training set to synthetically oversample the minority class.

**How to use:**
Feature engineering is located in `bank_marketing_pipeline.ipynb` under **Cell 3**. Run this cell to encode categories, perform the 70/30 split, and apply SMOTE.
