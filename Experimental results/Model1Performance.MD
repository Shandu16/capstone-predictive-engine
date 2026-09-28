# Model 1 Performance: XGBoost Classifier

**Related Script:** `bank_marketing_pipeline.ipynb`
**How to use:** Open the notebook and run **Cell 4** for basic metrics and **Cell 6** for advanced statistical evaluations.

## Performance Metrics & Statistical Measures
Based on the classification report and confusion matrix generated on the test set, the XGBoost model achieved the following:

* **Overall Accuracy:** 88.52%
* **Minority Class (1) Precision:** 0.49
* **Minority Class (1) Recall:** 0.51
* **ROC-AUC Score:** 0.7994

## Statistical Analysis
The XGBoost model demonstrates strong overall accuracy (88.52%),
but this metric is heavily skewed by the majority class (Class 0), which it predicts with high confidence. 

When evaluating the model's ability to identify the minority class (Class 1), the performance drops.
A precision of 0.49 indicates that when the model predicts a positive instance, it is correct less than half the time.
More importantly, the recall of 0.51 means the model is missing 49% of the actual positive cases (false negatives). 
The ROC-AUC score of 0.7994[cite: 12] and Confusion Matrix (showing 685 false negatives against 707 true positives) 
further highlight that while the model separates classes reasonably well, its threshold natively favors the majority class,
leading to a high rate of missed targets in a business context.
