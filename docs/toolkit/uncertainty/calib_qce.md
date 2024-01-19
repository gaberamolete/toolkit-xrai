---
layout: default
title: XRAIDashboard.uncertainty.calibration.calib_qce
parent: Uncertainty
grand_parent: Toolkit
has_children: false
nav_order: 14
---

# XRAIDashboard.uncertainty.calibration.calib_qce
**[XRAIDashboard.uncertainty.calibration.calib_qce(y_pred_means, y_pred_stds, y_true, bins = 10, quantiles = np.linspace(0.1, 0.9, 10 - 1),reduction = 'mean')](https://github.com/gaberamolete/XRAIDashboard/blob/main/uncertainty/calibration.py)**


Quantile Calibration Error (QCE), a quantile-based calibration. Returns the Marginal Quantile Calibration Error (M-QCE), which measures the gap between predicted quantiles and observed quantile coverage for multivariate distributions. This is based on the Normalized Estimation Error Squared (NEES), known from object tracking.


**Parameters:**
- y_pred_means (numpy.ndarray): Array or series of predicted values.
- y_pred_stds (numpy.ndarray)
- y_true (numpy.ndarray): Array or Series with ground truth labels.
- bins (int): Number of bins used for the internal binning. Defaults to 10.
- quantiles (numpy.ndarray): Array of quantile scores in [0, 1] of size q to compute the x-valued quantile boundaries for.
- reduction (str): one of 'none', 'mean', or 'sum', default: 'mean'
    - Specifies the reduction to apply to the output:
        - none : no reduction is performed. Return NLL for each sample and for each dim separately.
        - mean : calculate mean over all samples and all dimensions.
        - sum : calculate sum over all samples and all dimensions.


**Returns:**
- qce_score: Marginal Quantile Calibration Error

