---
layout: default
title: XRAIDashboard.stability.stability.ks
parent: Stability
grand_parent: Toolkit
nav_order: 1
---

# XRAIDashboard.stability.stability.ks
**[XRAIDashboard.stability.stability.ks(train, test, p_value=0.05)](https://github.com/gaberamolete/XRAIDashboard/blob/main/stability/stability.py)**


The K-S test is a nonparametric test that compares the cumulative distributions of two data sets, in this case, the training data and the post-training data. The null hypothesis for this test states that the data distributions from both the datasets are same. If the null is rejected then we can conclude that there is adrift in the model.


**Parameters:**
- train: pd.DataFrame
- test: pd.DataFrame
- p_value: float, defaults to 0.05

**Returns:**
- ks_df: DataFrame containing the solve p_values
- rejected_cols: List of string of columns rejected based on the defined `p_value` threshold