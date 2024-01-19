---
layout: default
title: XRAIDashboard.global_exp.global_exp.shap_force_glob
parent: Global Explainability
grand_parent: Toolkit
nav_order: 1
---

# XRAIDashboard.global_exp.global_exp.shap_force_glob
**[XRAIDashboard.global_exp.global_exp.shap_force_glob(explainer, shap_values, X_proc, feature_names = None, class_ind = None, class_names = None, samples = 100, reg = False)](https://github.com/gaberamolete/XRAIDashboard/blob/main/global_exp/global_exp.py)**


Returns an interactive global force plot.


**Parameters:**
- explainer: Shap explainer object generated in the initial instance.
- shap_values: Array of shap values used for the force plot graph. Generated from the initial global shap instance.
- X_proc: Processed X DataFrame used in line with the shap values.
- feature_names: List of features that correspond to the column indices in X_proc. Defaults to None, but is highly recommended for explainability purposes.
- class_ind: int, represents index used for classification objects in determining which shap values to show. Regression models do not need this variable. Defaults to None.
- class_names: List of all class names of target feature under a classification model. This will be used with the `class_ind` to indicate what class is being shown. Defaults to None.
- samples: int, number of samples to be included in the global force plot explanation. Defaults to 100.
- reg: Indicates whether model with which `shap_values` and `X_proc` was trained on is a regression or classification model. Defaults to False.
    

**Returns:**
- shap_html: Raw html of shap force plot.

*Note: The SHAP force global plot will be displayed by this function in the notebook. Prerequisite: run `shap.initjs()`.*