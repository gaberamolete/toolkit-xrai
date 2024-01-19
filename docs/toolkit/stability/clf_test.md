---
layout: default
title: XRAIDashboard.stability.stability.classification_performance_test
parent: Stability
grand_parent: Toolkit
nav_order: 1
---

# XRAIDashboard.stability.stability.classification_performance_test
**[XRAIDashboard.stability.stability.classification_performance_test(current_data, reference_data, test_format = 'json', column_mapping = None,probas_threshold = None, pred_col = 'prediction', approx_val = None, rel_val = 0.2, test_proba=None)](https://github.com/gaberamolete/XRAIDashboard/blob/main/stability/stability.py)**

    
Computes the following tests on classification data, failing if +/- a percentage (%) of scores over reference data is achieved:
    - Accuracy, Precision, Recall, F1 on the whole dataset
    - Precision, Recall, F1 on each class
    - Computes the True Positive Rate (TPR), True Negative Rate (TNR), False Positive Rate (FPR), False Negative Rate (FNR)
    - For probabilistic classification, computes the ROC AUC and LogLoss


**Parameters:**
- current_data: DataFrame, inference data collected after model deployment or training.
- reference_data: DataFrame, dataset used to train your initial model on.
- test_format: Specify the format to output the test object in, from `json`, `dict`, and `DataFrame`. Defaults to `json`.
- column_mapping: Input a column mapping object so the function knows how to treat each column based on data type. Defaults to None.
- probas_threshold: Threshold at which to determine a positive value for a class. Defaults to None. Can be set to 0.5 for probabilistic classification.
- pred_col: Column name of prediction column in current data. Defaults to `prediction`.
- approx_val: Dictionary, if user wants to specify values for each test. Defaults to None. See documentation for example on how to put parameters.
- rel_val: Relative percentage with which each test will pass or fail. Defaults to 0.2 (20%).

**Returns:**
- classification_test: Interactive visualization object containing the classification test
- cpt: test 