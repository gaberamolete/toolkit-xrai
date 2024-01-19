---
layout: default
title: XRAIDashboard.global_exp.global_exp.shap_summary
parent: Global Explainability
grand_parent: Toolkit
nav_order: 1
---

# XRAIDashboard.global_exp.global_exp.shap_summary
**[XRAIDashboard.global_exp.global_exp.shap_summary(shap_value_glob, idx, feature_names = None, class_ind = None, class_names = None, reg = False, show=True)](https://github.com/gaberamolete/XRAIDashboard/blob/main/global_exp/global_exp.py)**


Returns a Shap density summary plot.


**Parameters:**
- shap_value_glob: Array of shap values used for the waterfall plot. Generated from the initial global shap instance.
- idx: Index to be used for global observation.
- feature_names: List of features that correspond to the column indices in `shap_value_glob`. Defaults to None, but is highly recommended for explainability purposes.
- class_ind: int, represents index used for classification objects in determining which shap values to show. Regression models do not need this variable. Defaults to None.
- class_names: List of all class names of target feature under a classification model. This will be used with the `class_ind` to indicate what class is being shown. Defaults to None.
- reg: Indicates whether model with which `shap_values_glob` was trained on is a regression or classification model. Defaults to False.
- show: Show the plot or not. Defaults to True.

**Returns:**
- s: Shap summary plot figure.