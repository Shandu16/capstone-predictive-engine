# Data Preprocessing

**Related Script:** `STADIO_activation_pipeline.ipynb`

*Techniques Applied:
1. **Target Variable Separation:** Isolating the `is_funded` variable from the feature set.
2. **Data Leakage Removal:** Dropping columns that are populated post-event (e.g., `first_deposit_ts`, `initial_deposit_zar`, `client_id`).
3. **Numerical Scaling:** Using Scikit-Learn's `StandardScaler` to normalize numerical features like `client_age`, `session_duration_sec`, and `kyc_time_spent_sec` to have a mean of 0 and a variance of 1, preventing features with larger magnitudes from dominating the models.

**How to use:**
All preprocessing is implemented in `STADIO_activation_pipeline.ipynb` under **Cell 2 (Preprocessing)**. Open the notebook and run Cell 1 and Cell 2 to load the dataset and scale numerical features.
