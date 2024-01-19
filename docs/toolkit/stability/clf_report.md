---
layout: default
title: XRAIDashboard.stability.stability.classification_performance_report
parent: Stability
grand_parent: Toolkit
nav_order: 1
---

# XRAIDashboard.stability.stability.classification_performance_report
**[XRAIDashboard.stability.stability.classification_performance_report(current_data, reference_data, report_format = 'json', column_mapping = None,probas_threshold = None, columns = None)](https://github.com/gaberamolete/XRAIDashboard/blob/main/stability/stability.py)**

    
For a classification model, the report shows the following:
- Calculates various classification performance metrics, such as precision, accuracy, recall, F1-score, TPR, TNR, FPR, FNR, AUROC, LogLoss
- Calculates the number of objects for each label and plots a histogram
- Calculates the TPR, TNR, FPR, FNR, and plots the confusion matrix
- Calculates the classification quality metrics for each class and plots a matrix
- For probabilistic classification, visualizes the predicted probabilities by class
- For probabilistic classification, visualizes the probability distribution by class
- For probabilistic classification, plots the ROC Curve
- For probabilistic classification, plots the Precision-Recall curve
- Calculates the Precision-Recall table that shows model quality at a different decision threshold
- Visualizes the relationship between feature values and model quality


**Parameters:**
- current_data: DataFrame, inference data collected after model deployment or training.
- reference_data: DataFrame, dataset used to train your initial model on.
- report_format: Specify the format to output the report object in, from `json`, `dict`, and `DataFrame`. Defaults to `json`.
- column_mapping: Input a column mapping object so the function knows how to treat each column based on data type. Defaults to None.
- probas_threshold: Threshold at which to determine a positive value for a class. Defaults to None. Can be set to 0.5 for probabilistic classification.
- columns: List of columns to showcase in the error bias table. Defaults to None, which showcases all columns.

**Returns:**
- classification_report: Interactive visualization object containing the classification report
- cpr: Report 