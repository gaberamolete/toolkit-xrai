---
layout: default
title: XRAIDashboard.local_exp.local_exp.dice_exp
parent: Local Explainability
grand_parent: Toolkit
nav_order: 1
---

# XRAIDashboard.local_exp.local_exp.dice_exp
**[XRAIDashboard.local_exp.local_exp.dice_exp(X_train, y_train, model, target, backend = 'sklearn', model_type = 'classifier')](https://github.com/gaberamolete/XRAIDashboard/blob/main/local_exp/local_exp.py)**


Initialize dice experiment CF.


**Parameters:**
- X_train (pandas.DataFrame): X_train
- y_train (pandas.DataFrame or pandas.Series): Contains target column and list of target variables
- model (model object): Can be sklearn, tensorflow, or keras
- target (str): Name of target variable
- backend (str): "TF1" ("TF2") for TensorFLow 1.0 (2.0), "PYT" for PyTorch implementations, "sklearn" for Scikit-Learn implementations of standard DiCE (https://arxiv.org/pdf/1905.07697.pdf). For all other frameworks and implementations, provide a dictionary with "model" and "explainer" as keys, and include module and class names as values in the form module_name.class_name. For instance, if there is a model interface class "XGBoostModel" in module "xgboost_model.py" inside the subpackage dice_ml.model_interfaces, and dice interface class "DiceXGBoost" in module "dice_xgboost" inside dice_ml.explainer_interfaces, then backend parameter should be {"model": "xgboost_model.XGBoostModel", "explainer": dice_xgboost.DiceXGBoost}.
- model_type (str): classifier or regressor

**Returns:**
- exp (dice_ml.Explanation): Explanation object for DICE local explanation
