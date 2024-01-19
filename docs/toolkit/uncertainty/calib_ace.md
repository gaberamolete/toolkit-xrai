---
layout: default
title: XRAIDashboard.uncertainty.calibration.calib_ace
parent: Uncertainty
grand_parent: Toolkit
has_children: false
nav_order: 10
---

# XRAIDashboard.uncertainty.calibration.calib_ace
**[XRAIDashboard.uncertainty.calibration.calib_ace(y_pred, y_true, n_bins = 10, equal_intervals: bool = True, sample_threshold: int = 1, reg = False)](https://github.com/gaberamolete/XRAIDashboard/blob/main/uncertainty/calibration.py)**


Average Calibration Error (ACE), denotes the average miscalibration where each bin gets weighted equally.


**Parameters:**
- y_pred (numpy.ndarray): Array or series of predicted values.
- y_true (numpy.ndarray): Array or Series with ground truth labels.
- n_bins (int): Number of bins used for the internal binning. Defaults to 10.
- equal_intervals (bool): If True, the bins have the same width. If False, the bins are splitted to equalize the number of samples in each bin. Defaults to True.
- sample_threshold (int): no. of bins with an amount of samples below this threshold are not included into the miscalibration. Defaults to 1.
- reg (bool): Determines if y's given are from a regression or classification problem. Defaults to False.

**Returns:**
- ace_score: Average Calibration Error
