---
layout: default
title: XRAIDashboard.fairness.fairness.model_performance
parent: Fairness & Performance
grand_parent: Toolkit
nav_order: 1
---

# XRAIDashboard.fairness.fairness.model_performance
**[XRAIDashboard.fairness.fairness.model_performance(model,test_x,test_y,train_x,train_y,all_test,all_train, target_feature ,protected_groups, reg=False)](https://github.com/gaberamolete/XRAIDashboard/blob/main/fairness/fairness.py)**


Evaluate the performance of the model on the widely used performance metrics for regression and classification.


**Parameters:**
- model (dict): list of models,model object, can be sklearn, tensorflow, or keras
- test_x (pandas.DataFrame): X_test
- test_y (pandas.DataFrame): y_test
- target_feature (str): name of target variable
- protected_groups (dict): dictionary of protected groups and protected category in that group, example: {"LGU" : 'pasay','income_class':"1st" }
- reg (bool): Boolean for model type of Regression

**Returns:**
- result_sum_test (pandas.DataFrame): contains the result of the model on the test set against the performance metrics
- result_sum_train (pandas.DataFrame): contains the result of the model on the train set against the performance metrics
