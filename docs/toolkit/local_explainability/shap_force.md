---
layout: default
title: XRAIDashboard.local_exp.local_exp.shap_force_loc
parent: Local Explainability
grand_parent: Toolkit
nav_order: 1
---

# XRAIDashboard.local_exp.local_exp.shap_force_loc
**[XRAIDashboard.local_exp.local_exp.shap_force_loc(shap_value_loc, idx, feature_names = None, class_ind = None, class_names = None, reg = False, show=True)](https://github.com/gaberamolete/XRAIDashboard/blob/main/local_exp/local_exp.py)**


Returns a shap force plot for a specified observation.


**Parameters:**
- shap_value_loc: Array of shap values used for the waterfall plot. Generated from the initial local shap instance.
- idx: Index to be used for local observation.
- feature_names: List of features that correspond to the column indices in `shap_value_loc`. Defaults to None, but is highly recommended for explainability purposes.
- class_ind: int, represents index used for classification objects in determining which shap values to show. Regression models do not need this variable. Defaults to None.
- class_names: List of all class names of target feature under a classification model. This will be used with the `class_ind` to indicate what class is being shown. Defaults to None.
- reg: Indicates whether model with which `shap_values_loc` was trained on is a regression or classification model. Defaults to False.
- show: Show the plot or not. Defaults to True.

**Returns:**
- s: Shap local force plot figure.