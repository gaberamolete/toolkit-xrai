---
layout: default
title: XRAIDashboard.stability.stability.fishers_exact_test
parent: Stability
grand_parent: Toolkit
nav_order: 1
---

# XRAIDashboard.stability.stability.fishers_exact_test
**[XRAIDashboard.stability.stability.fishers_exact_test(loss_ref, losses, p_val = 0.05, labels = ['No!', 'Yes!'])](https://github.com/gaberamolete/XRAIDashboard/blob/main/stability/stability.py)**

    
Fisher exact test (FET) data drift detector, which tests for a change in the mean of binary univariate data. Works for classification use cases only. For multivariate data, a separate FET test is applied to each feature, and the obtained p-values are aggregated via the Bonferroni or False Discovery Rate (FDR) corrections.


**Parameters:**
-  loss_ref: Loss function from your reference data
-  losses: Dictionary, with key-value pair of `Dataset` and `loss function for that dataset`. Examples of what could be tested are {`Concept`: loss_concept, `Covariance`: loss_covariance, `6MonthsPast`: loss_6months}
-  p_val: Threshold to determine whether data has drifted. Defaults to 0.05.
-  labels: List, labels to detect drift. Defaults to ['No', 'Yes'].

**Returns:**
- fet_dict: Dictionary of datasets and p-values based on the Fisher's Exact Test detector