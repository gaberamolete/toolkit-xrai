---
layout: default
title: XRAIDashboard.stability.stability.categs
parent: Stability
grand_parent: Toolkit
nav_order: 1
---

# XRAIDashboard.stability.stability.categs
**[XRAIDashboard.stability.stability.categs(X, infer = False)](https://github.com/gaberamolete/XRAIDashboard/blob/main/stability/stability.py)**

    
Generate a category map, and the categories on each categorical feature. For Alibe-Detect Functions.


**Parameters:**
-  X: DataFrame of variables used to train model
-  infer: Boolean, if you want the TabularDrift detector to infer the number of categories from reference data. Defaults to False.

**Returns:**
- df_cat_map: DataFrame category mapping