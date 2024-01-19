---
layout: default
title: XRAIDashboard.robustness.art_metrics.SHAPr_metric
parent: Robustness
grand_parent: Toolkit
nav_order: 1
---

# XRAIDashboard.robustness.art_metrics.SHAPr_metric
**[XRAIDashboard.robustness.art_metrics.SHAPr_metric(x_train, y_train, x_test, y_test, art_extra_classifiers_dict, key, threshold_value)](https://github.com/gaberamolete/XRAIDashboard/blob/main/robustness/art_metrics.py)**

    
Calculates the SHAPr metric for a given classifier and dataset


**Parameters:**
- x_train: pd.DataFrame
- y_train: pd.DataFrame
- x_test: pd.DataFrame
- y_test: pd.DataFrame
- art_extra_classifiers_dict: dictionary of ART classifiers and extra classifiers for the given models. Key is the name of given model
- key: string of model name

**Returns:**
- SHAPr_art: List of scores for SHAPr for all samples
- bool: Whether the value is above or below threshold