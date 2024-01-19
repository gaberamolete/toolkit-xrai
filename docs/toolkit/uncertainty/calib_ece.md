---
layout: default
title: XRAIDashboard.uncertainty.calibration.calib_ece
parent: Uncertainty
grand_parent: Toolkit
has_children: false
nav_order: 8
---

# XRAIDashboard.uncertainty.calibration.calib_ece
**[XRAIDashboard.uncertainty.calibration.calib_ece(y_pred, y_true, n_bins = 10, equal_intervals: bool = True, sample_threshold: int = 1, reg = False)](https://github.com/gaberamolete/XRAIDashboard/blob/main/uncertainty/calibration.py)**


Expected Calibration Error (ECE), which divides the confidence space into several bins and measures the observed accuracy in each bin. The bin gaps between observed accuracy and bin confidence are summed up and weighted by the amount of samples in each bin.


**Parameters:**
- y_pred (numpy.ndarray): Array or series of predicted values.
- y_true (numpy.ndarray): Array or Series with ground truth labels.
- n_bins (int): Number of bins used for the internal binning. Defaults to 10.
- equal_intervals (bool): If True, the bins have the same width. If False, the bins are splitted to equalize the number of samples in each bin. Defaults to True.
- sample_threshold (int): no. of bins with an amount of samples below this threshold are not included into the miscalibration. Defaults to 1.
- reg (bool): Determines if y's given are from a regression or classification problem. Defaults to False.

**Returns:**
- ece_score: Expected Calibration Error
