---
layout: default
title: XRAIDashboard.global_exp.global_exp.var_imp
parent: Global Explainability
grand_parent: Toolkit
nav_order: 1
---

# XRAIDashboard.global_exp.global_exp.var_imp
**[XRAIDashboard.global_exp.global_exp.var_imp(exp, loss_function = 'rmse', groups = None, N = 1000, B = 10, random_state = 42)](https://github.com/gaberamolete/XRAIDashboard/blob/main/global_exp/global_exp.py)**


A permutation-based approach in explaining variable importance to the model.


**Parameters:**
-  exp: explanation object
- loss_function: manner in which the function will calculate loss. Can choose from 'rmse', 'mae', 'mse', 'mad', '1-auc'. Defaults to 'rmse'.
- groups: specify a single categorical variable not in the 'variables' list that will be used as a group. Defaults to 'None'.
- N: Number of observations to be sampled with. Defaults to 1900. Writing 'None' will have the function use all data, which may be computationally expensive.
- B: Number of permutation rounds to be perform on each variable. Defaults to 10.
- random_state: defines the random state in which the number of observations to be sampled. Defaults to 42 for reproducibility.

**Returns:**
- result: DataFrame of the results from the variable importance plot.
- plot: plotly.Figure for the visualization