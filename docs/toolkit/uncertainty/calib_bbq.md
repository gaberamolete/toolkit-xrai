---
layout: default
title: XRAIDashboard.uncertainty.calibration.calib_bbq
parent: Uncertainty
grand_parent: Toolkit
nav_order: 6
---

# XRAIDashboard.uncertainty.calibration.calib_bbq
**[XRAIDashboard.uncertainty.calibration.calib_bbq(y_pred,y_true,reg)](https://github.com/gaberamolete/XRAIDashboard/blob/main/uncertainty/calibration.py)**


Bayesian Binning into Quantiles (BBQ). Utilizes multiple Histogram Binning instances with different amounts of bins, and computes a weighted sum of all methods to obtain a well-calibrated confidence estimate. Not recommended for regression outputs.


**Parameters:**
- y_pred (numpy.ndarray): Array or series of predicted values.
- y_true (numpy.ndarray): Array or Series with ground truth labels.
- reg (bool): Determines if y's given are from a regression or classification problem. Defaults to False.

**Returns:**
- bbq: Bayesian Binning into Quantiles object.
- bbq_calibrated: Recalibrated values under Bayesian Binning into Quantiles, given via array.
