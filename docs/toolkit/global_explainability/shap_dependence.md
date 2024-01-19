---
layout: default
title: XRAIDashboard.global_exp.global_exp.shap_dependence
parent: Global Explainability
grand_parent: Toolkit
nav_order: 1
---

# XRAIDashboard.global_exp.global_exp.shap_dependence
**[XRAIDashboard.global_exp.global_exp.shap_dependence(shap_values, X_proc, shap_ind, feature_names = None, class_ind = None, class_names = None, int_ind = None, reg = False)](https://github.com/gaberamolete/XRAIDashboard/blob/main/global_exp/global_exp.py)**


Returns a dependence plot comparing a value and its equivalent shap values. The user may also compare these with another variable as an interaction index.


**Parameters:**
-  shap_values: Array of shap values used for the dependence plot graph. Generated from the initial global shap instance.
- X_proc: Processed X DataFrame used in line with the shap values.
- shap_ind: Feature to compare with. Ideally should be a column name from the `feature_names` list, but can also just be an integer corresponding to said index.
- feature_names: List of features that correspond to the column indices in X_proc. Defaults to None, but is highly recommended for explainability purposes.
- class_ind: int, represents index used for classification objects in determining which shap values to show. Regression models do not need this variable. Defaults to None.
- class_names: List of all class names of target feature under a classification model. This will be used with the `class_ind` to indicate what class is being shown. Defaults to None.
- int_ind: The index of the feature used to color the plot. The name of a feature can also be passed as a string. If "auto" then shap.common.approximate_interactions is used to pick what seems to be the strongest interaction. Defaults to None.
- reg: Indicates whether model with which `shap_values` and `X_proc` was trained on is a regression or classification model. Defaults to False.
    

**Returns:**
- s: Shap dependence plot figure.