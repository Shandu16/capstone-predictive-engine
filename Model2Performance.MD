# Model 2 Performance: Random Forest Classifier

**Related Script:** `bank_marketing_pipeline.ipynb`
**How to use:** Open the notebook and run **Cell 5** for basic metrics and **Cell 7** for advanced statistical evaluations.

## Performance Metrics & Statistical Measures
Based on the test set evaluation, the Random Forest model (with balanced class weighting) achieved the following results:

* **Overall Accuracy:** 86.74%
* **Minority Class (1) Precision:** 0.44
* **Minority Class (1) Recall:** 0.62
* **ROC-AUC Score:** 0.8077

## Statistical Analysis
The Random Forest model exhibits an overall accuracy of 86.74%, a slight decrease from Model 1.
However, the application of balanced class weights drastically shifted the model's statistical priorities. 

The most critical statistical measure here is the Class 1 Recall, which jumped to 0.62.
This indicates that the model successfully identifies 62% of all actual positive cases.
The trade-off is a lower precision for Class 1 (0.44), meaning the model casts a wider net and captures more false positives,
generating 1,107 false positives according to the confusion matrix. The ROC-AUC score of 0.8077 confirms that despite the lower accuracy,
this model possesses a mathematically superior ability to distinguish between the two classes. For highly imbalanced datasets
where missing a true positive is costly, this model's statistical bias toward higher recall is preferable.
