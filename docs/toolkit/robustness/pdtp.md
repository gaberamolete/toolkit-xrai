---
layout: default
title: XRAIDashboard.robustness.art_metrics.pdtp_metric
parent: Robustness
grand_parent: Toolkit
nav_order: 1
---

# XRAIDashboard.robustness.art_metrics.pdtp_metric
**[XRAIDashboard.robustness.art_metrics.pdtp_metric(x_train, y_train, art_extra_classifiers_dict, key, threshold_value, sample_indexes, num_iter=10)](https://github.com/gaberamolete/XRAIDashboard/blob/main/robustness/art_metrics.py)**

    
Calculates the PDTP metric for a given classifier and dataset and whether PDTP breaches the threshold value 


**Parameters:**
- x: pd.DataFrame
- y: pd.DataFrame
- art_extra_classifiers: dictionary of ART classifiers and extra classifiers for the given models. Key is the given model
- key: string of model name
- num_samples: number of samples to compute PDTP on. If not supplied, PDTP will be computed for 50 samples in x.
- num_iter(int): the number of iterations of PDTP computation to run for each sample. If not supplied, defaults to 10. The result is the average across iterations.

**Returns:**
- pdtp_art: List of scores for PDTP for all samples
- bool: Whether the value is above or below threshold
- sample_indexes: List index of the samples