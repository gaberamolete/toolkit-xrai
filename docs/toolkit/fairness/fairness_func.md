---
layout: default
title: XRAIDashboard.fairness.fairness.fairness
parent: Fairness & Performance
grand_parent: Toolkit
nav_order: 1
---

# XRAIDashboard.fairness.fairness.fairness
**[XRAIDashboard.fairness.fairness.fairness(models,x,y,protected_groups={},metric="DI", threshold=0.8, xextra=False,reg=False,dashboard=True)](https://github.com/gaberamolete/XRAIDashboard/blob/main/fairness/fairness.py)**


Evaluate the fairness of the model on the widely used fairness metrics for regression and classification.


**Parameters:**
- models (dict): list of models,model object, can be sklearn, tensorflow, or keras
- x (pandas.DataFrame): X_test
- y (pandas.DataFrame): y_test
- protected_groups (dict): dictionary of protected groups and protected - - category in that group, example: {"LGU" : 'pasay','income_class':"1st" }
- metric (str): DI, EOP, or EOD
- threshold (float): how far from the ideal value could the score from the fairness metrics be
- xextra (pandas.DataFrame): to include any columns that was dropped by the model
- reg (bool): boolean for model type of Regression
- dashboard (bool): if this is for the dashboard purposes

**Returns:**
- if reg==False
    - fairness_index (float): score on the fairness metric
    - fairness_report (pandas.DataFrame): the performance of the model in different metrics
    - a (numpy.ndarray): for the purpose of plotting the confusion matrix of the model
- if reg==True
    - contents_list (List): text containing the summary performance of the model to the fairness metrics (listed to accomodate analysis of more than one model)
    - fig1_list (List): horizontal bar plot visualizing the score on the fairness metrics (listed to accomodate analysis of more than one model)
    - fig2_list (List): horizontal violin plot visualizing the density of the data (listed to accomodate analysis of more than one model)
