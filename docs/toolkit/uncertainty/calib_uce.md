---
layout: default
title: XRAIDashboard.uncertainty.calibration.calib_uce
parent: Uncertainty
grand_parent: Toolkit
has_children: false
nav_order: 16
---

# XRAIDashboard.uncertainty.calibration.calib_uce
**[XRAIDashboard.uncertainty.calibration.calib_uce(y_pred_means, y_pred_stds, y_true, bins = 10)](https://github.com/gaberamolete/XRAIDashboard/blob/main/uncertainty/calibration.py)**


Uncertainty Calibration Error (UCE), a variance-based calibration. Used for normal distributions, where we measure the quality of the predicted variance/stddev estimates. We require that the predicted variance matches the observed error variance, which is equivalent to the Mean Squared Error. UCE applies a binning scheme with  𝐵 bins over the predicted variance  𝜎2𝑦(𝑋) and measures the absolute difference between MSE and MV. 


**Parameters:**
- y_pred_means (numpy.ndarray): Array or series of predicted values.
- y_pred_stds (numpy.ndarray)
- y_true (numpy.ndarray): Array or Series with ground truth labels.
- bins (int): Number of bins used for the internal binning. Defaults to 10.


**Returns:**
uce_score: Uncertainty Calibration Error

