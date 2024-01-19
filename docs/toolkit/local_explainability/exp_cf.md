---
layout: default
title: XRAIDashboard.local_exp.local_exp.exp_cf
parent: Local Explainability
grand_parent: Toolkit
nav_order: 1
---

# XRAIDashboard.local_exp.local_exp.exp_cf
**[XRAIDashboard.local_exp.local_exp.exp_cf(X, exp, total_CFs = 2, desired_range = None, desired_class = 'opposite', features_to_vary = 'all',permitted_range = None, reg = False)](https://github.com/gaberamolete/XRAIDashboard/blob/main/local_exp/local_exp.py)**


Generates counterfactuals.


**Parameters:**
- X (pandas.DataFrame): Rows of dataset to be analyzed via CF
- exp (dice_ml.Explanation): Object created by dice_exp()
- total_CFs (int): Number of CFs to be generated
- desired_range (List): Range of desired output for regression case
- desired_class (int or str): Desired CF class - can take 0 or 1. Default value is 'opposite' to the outcome class of query_instance for binary classification. Specify the class name for non-binary classification.
- features_to_vary (List(str)): List of names of features to vary. Defaults to all.
- permitted_range (dict): Dictionary with key-value pairs of variable name and ranges. Defaults to None.
- reg (bool): Regression use case or not

**Returns:**
- e (pandas.DataFrame): Generated counterfactuals
