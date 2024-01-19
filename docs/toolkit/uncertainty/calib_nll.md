---
layout: default
title: XRAIDashboard.uncertainty.calibration.calib_nll
parent: Uncertainty
grand_parent: Toolkit
has_children: false
nav_order: 11
---

# XRAIDashboard.uncertainty.calibration.calib_nll
**[XRAIDashboard.uncertainty.calibration.calib_nll(y_pred_means, y_pred_stds, y_true, reduction = 'mean')](https://github.com/gaberamolete/XRAIDashboard/blob/main/uncertainty/calibration.py)**


Negative Log Likelihood, measures the quality of a predicted probability distribution with respect to the ground truth.


**Parameters:**
- y_pred_means (numpy.ndarray): Array or series of predicted values.
- y_pred_stds (numpy.ndarray)
- y_true (numpy.ndarray): Array or Series with ground truth labels.
- reduction (str): one of 'none', 'mean', 'batchmean', 'sum' or 'batchsum', default: 'mean'
    - Specifies the reduction to apply to the output:
        - none : no reduction is performed. Return NLL for each sample and for each dim separately.
        - mean : calculate mean over all samples and all dimensions.
        - batchmean : calculate mean over all samples but for each dim separately. If input has covariance matrices, 'batchmean' is the same as 'mean'.
        - sum : calculate sum over all samples and all dimensions.
        - batchsum : calculate sum over all samples but for each dim separately. If input has covariance matrices, 'batchsum' is the same as 'sum'.

**Returns:**
- nll_score: Negative Log Likelihood
