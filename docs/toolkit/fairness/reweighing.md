---
layout: default
title: XRAIDashboard.fairness.fairness_algorithm.reweighing
parent: Fairness & Performance
grand_parent: Toolkit
nav_order: 4
---

# XRAIDashboard.fairness.fairness_algorithm.reweighing
**[XRAIDashboard.fairness.fairness_algorithm.reweighing(model, train_data, test_data, target_feature, protected, privileged_classes, favorable_classes=[1.0])](https://github.com/gaberamolete/XRAIDashboard/blob/main/fairness/fairness_algorithm.py)**


Executes use of AI Fairness 360's Reweighing algorithm. Reweighing is a preprocessing technique that Weights the examples in each (group, label) combination differently to ensure fairness before classification.


**Parameters:**
-  model: the classifier model object
- train_data (pd.DataFrame): the train split from the dataset, must be preprocessed beforehand
- test_data (pd.DataFrame): the test split from the dataset, must be preprocessed beforehand
- target_feature (str): the target feature
- protected (list): list of protected features
- privileged_classes (list(list)): a 2d list containing the privileged classes for each protected feature
- favorable_classes (list): a list of favorable classes in the target feature, restricted to n-1 length, where n is the number of classes

**Returns:**
- X_tr (np.array): Transformed X_train

*Note: This outputs a comparison (w/ visualization) of the score of metrics before and after the method was used.*