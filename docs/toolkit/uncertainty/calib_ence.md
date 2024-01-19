---
layout: default
title: XRAIDashboard.uncertainty.calibration.calib_ence
parent: Uncertainty
grand_parent: Toolkit
has_children: false
nav_order: 15
---

# XRAIDashboard.uncertainty.calibration.calib_ence
**[XRAIDashboard.uncertainty.calibration.calib_ence(y_pred_means, y_pred_stds, y_true, bins = 10)](https://github.com/gaberamolete/XRAIDashboard/blob/main/uncertainty/calibration.py)**


Expected Normalized Calibration Error (ENCE), a variance-based calibration. Used for normal distributions, where we measure the quality of the predicted variance/stddev estimates. We require that the predicted variance matches the observed error variance, which is equivalent to the Mean Squared Error. ENCE applies a binning scheme with  𝐵 bins over the predicted standard deviation  𝜎𝑦(𝑋) and measures the absolute (normalized) difference between RMSE and RMV.


**Parameters:**
- y_pred_means (numpy.ndarray): Array or series of predicted values.
- y_pred_stds (numpy.ndarray)
- y_true (numpy.ndarray): Array or Series with ground truth labels.
- bins (int): Number of bins used for the internal binning. Defaults to 10.


**Returns:**
- ence_score: Expected Normalized Calibration Error

