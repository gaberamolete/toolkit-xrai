---
layout: default
title: XRAIDashboard.stability.stability.cramer_von_mises
parent: Stability
grand_parent: Toolkit
nav_order: 1
---

# XRAIDashboard.stability.stability.cramer_von_mises
**[XRAIDashboard.stability.stability.cramer_von_mises(loss_ref, losses, p_val = 0.05, labels = ['No!', 'Yes!'])](https://github.com/gaberamolete/XRAIDashboard/blob/main/stability/stability.py)**

    
Cramer-von Mises (CVM) data drift detector, which tests for any change in the distribution of continuous univariate data. Works for both regression and classification use cases. For multivariate data, a separate CVM test is applied to each feature, and the obtained p-values are aggregated via the Bonferroni or False Discovery Rate (FDR) corrections.


**Parameters:**
-  loss_ref: Loss function from your reference data
-  losses: Dictionary, with key-value pair of `Dataset` and `loss function for that dataset`. Examples of what could be tested are {`Concept`: loss_concept, `Covariance`: loss_covariance, `6MonthsPast`: loss_6months}
-  p_val: Threshold to determine whether data has drifted. Defaults to 0.05.
-  labels: List, labels to detect drift. Defaults to ['No', 'Yes'].

**Returns:**
- cvm_dict: Dictionary of datasets and p-values based on the Cramer-von-Mises detector