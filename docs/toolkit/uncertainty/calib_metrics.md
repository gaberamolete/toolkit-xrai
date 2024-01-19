---
layout: default
title: XRAIDashboard.uncertainty.calibration.calib_metrics
parent: Uncertainty
grand_parent: Toolkit
has_children: false
nav_order: 17
---

# XRAIDashboard.uncertainty.calibration.calib_metrics
**[XRAIDashboard.uncertainty.calibration.calib_metrics(y_true, calibs: Dict, n_bins = 100, reg = False)](https://github.com/gaberamolete/XRAIDashboard/blob/main/uncertainty/calibration.py)**


Outputs all calibration metrics for an array of predicted values. 


**Parameters:**
- y_true (numpy.ndarray): Array or series with ground truth labels..
- calibs (dict): Key-pair value of Calibration technique and calibrated values in array
- n_bins (int): Number of bins used for the internal binning. Defaults to 10.
- reg (bool): Determines if y's given are from a regression or classification problem. Defaults to False.

**Returns:**
- calibs_df (pandas.DataFrame): DataFrame of calculated calibration metrics on given calibration arrays

