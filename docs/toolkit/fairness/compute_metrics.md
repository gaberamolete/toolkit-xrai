---
layout: default
title: XRAIDashboard.fairness.fairness_algorithm.compute_metrics
parent: Fairness & Performance
grand_parent: Toolkit
nav_order: 4
---

# XRAIDashboard.fairness.fairness_algorithm.compute_metrics
**[XRAIDashboard.fairness.fairness_algorithm.compute_metrics(dataset_true, dataset_pred, unprivileged_groups, privileged_groups, disp = True)](https://github.com/gaberamolete/XRAIDashboard/blob/main/fairness/fairness_algorithm.py)**


Compute the fairness metrics for classification


**Parameters:**
- dataset_true (aif360.StandardDataset): The ground truth data
- dataset_pred (aif360.StandardDataset): The prediction data
- unprivileged_groups (List): List of unprivileged group
- privileged_groups (List): List of privileged group
- disp (bool): Print the metrics or not

**Returns:**
- metrics (OrderedDict): Dictionary of the different metrics and their corresponding scores.