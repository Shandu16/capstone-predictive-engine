# Model 2: Random Forest Classifier

**Related Script:** `bank_marketing_pipeline.ipynb`

**Model Details:**
* **Technique:** Random Forest. A bagging ensemble method that builds multiple decision trees to provide a robust, stable baseline comparison.
* **Hyperparameters:**
  * `n_estimators=100`: The number of trees in the forest.
  * `max_depth=10`: Limits tree depth to control overfitting.
  * `class_weight='balanced'`: Automatically adjusts weights inversely proportional to class frequencies.

**How to use:**
Implemented in `bank_marketing_pipeline.ipynb` under **Cell 5**. Run the cell to train the Random Forest model and view the evaluation metrics.
