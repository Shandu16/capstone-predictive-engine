# Model 1: XGBoost Classifier

**Related Script:** `bank_marketing_pipeline.ipynb`

**Model Details:**
* **Technique:** eXtreme Gradient Boosting (XGBoost). This tree-based ensemble method is highly effective for tabular classification tasks.
* **Hyperparameters:**
  * `n_estimators=100`: The number of boosting rounds.
  * `learning_rate=0.1`: Step size shrinkage to prevent overfitting.
  * `max_depth=5`: Restricts tree complexity.

**How to use:**
Implemented in `bank_marketing_pipeline.ipynb` under **Cell 4**. Run the cell to train the XGBoost model on the resampled data and output the classification report.
