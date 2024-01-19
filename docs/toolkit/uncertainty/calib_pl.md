---
layout: default
title: XRAIDashboard.uncertainty.calibration.calib_pl
parent: Uncertainty
grand_parent: Toolkit
has_children: false
nav_order: 12
---

# XRAIDashboard.uncertainty.calibration.calib_pl
**[XRAIDashboard.uncertainty.calibration.calib_pl(y_pred_means, y_pred_stds, y_true, reduction = 'mean')](https://github.com/gaberamolete/XRAIDashboard/blob/main/uncertainty/calibration.py)**


Pinball loss is a quantile-based calibration, and is a synonym for Quantile Loss. Tests for quantile calibration of a probabilistic regression model. This is an asymmetric loss that measures the quality of the predicted quantiles.


**Parameters:**
- y_pred_means (numpy.ndarray): Array or series of predicted values.
- y_pred_stds (numpy.ndarray)
- y_true (numpy.ndarray): Array or Series with ground truth labels.
- reduction (str): one of 'none', 'mean', or 'sum', default: 'mean'
    - Specifies the reduction to apply to the output:
        - none : no reduction is performed. Return NLL for each sample and for each dim separately.
        - mean : calculate mean over all samples and all dimensions.
        - sum : calculate sum over all samples and all dimensions.

**Returns:**
- pl_score: Pinball Loss
