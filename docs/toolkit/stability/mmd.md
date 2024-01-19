---
layout: default
title: XRAIDashboard.stability.stability.maximum_mean_discrepancy
parent: Stability
grand_parent: Toolkit
nav_order: 1
---

# XRAIDashboard.stability.stability.maximum_mean_discrepancy
**[XRAIDashboard.stability.stability.maximum_mean_discrepancy(X_ref, Xs, preprocessor = None, p_val = 0.05, labels = ['No!', 'Yes!'])](https://github.com/gaberamolete/XRAIDashboard/blob/main/stability/stability.py)**

    
Maximum Mean Discrepancy (MMD) data drift detector using a permutation test. Usually used for unsupervised, non-malicious drift detection. Works for regression, classification, and unsupervised use cases.


**Parameters:**
-  X_ref: DataFrame, containing the reference data used for model training.
-  Xs: Dictionary, with key-value pair of `Dataset Name` and `DataFrame`. Examples of what could be tested are {`Concept`: df_concept, `Covariance`: df_covariance, `6MonthsPast`: df_6months}
-  preprocessor: preprocessor object, if used to preprocessed data before model training. Defaults to None.
-  p_val: Threshold to determine whether data has drifted. Defaults to 0.05.
-  labels: List, labels to detect drift. Defaults to ['No', 'Yes'].

**Returns:**
- mmd_dict: Dictionary of datasets and p-values based on the Maximum Mean Discrepancy detector