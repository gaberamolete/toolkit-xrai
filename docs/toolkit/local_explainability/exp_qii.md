---
layout: default
title: XRAIDashboard.local_exp.local_exp.exp_qii
parent: Local Explainability
grand_parent: Toolkit
nav_order: 1
---

# XRAIDashboard.local_exp.local_exp.exp_qii
**[XRAIDashboard.local_exp.local_exp.exp_qii(model, X, idx, preprocessor = None, method = 'banzhaf', plot = True, pool_size = 100, n_samplings = 50, cat_cols = None)](https://github.com/gaberamolete/XRAIDashboard/blob/main/local_exp/local_exp.py)**


An alternate variable-importance measure using Quantity of Interest Method.


**Parameters:**
- model: Model object, must be model only and have preprocessing steps beforehand.
- X: DataFrame on which `model` trains on.
- idx: int, row of DataFrame/numpy.ndarray object to be observed.
- preprocessor: preprocessor object. Defaults to None.
- cat_cols: categorical columns found in X. Defaults to None.
- method: method of QII processing. Default is `banzhaf`, but can be `shapley`.
- plot: If user wants a plot of the QII values to be automatically generated. Defaults to True.
- pool_size: no. of instances to be sampled from. Defaults to 100.
- n_samplings: no. of samplings. Defaults to 50.

**Returns:**
- vals_df: DataFrame of features from preprocessed dataset and their corresponding QII (importance) variables.
- fig: Interactive figure object equivalent of `vals_df`.
