---
layout: default
title: XRAIDashboard.uncertainty.calibration.calib_picp
parent: Uncertainty
grand_parent: Toolkit
has_children: false
nav_order: 13
---

# XRAIDashboard.uncertainty.calibration.calib_picp
**[XRAIDashboard.uncertainty.calibration.calib_picp(y_pred_means, y_pred_stds, y_true, quantiles = np.linspace(0.1, 0.9, 10 - 1), reduction = 'mean')](https://github.com/gaberamolete/XRAIDashboard/blob/main/uncertainty/calibration.py)**


Prediction Interval Coverage Probability (PICP), a quantile-based calibration. The is used for Bayesian models to determine quality of the uncertainty estimates. In Bayesian mode, an uncertainty estimate is attached to each sample. The PICP measures the probability that the true (observed) accuracy falls into the  𝑝% prediction interval. Returns the PICP and the Mean Prediction Interval Width (MPIW).


**Parameters:**
- y_pred_means (numpy.ndarray): Array or series of predicted values.
- y_pred_stds (numpy.ndarray)
- y_true (numpy.ndarray): Array or Series with ground truth labels.
- quantiles (numpy.ndarray): Array of quantile scores in [0, 1] of size q to compute the x-valued quantile boundaries for.
- reduction (str): one of 'none', 'mean', or 'sum', default: 'mean'
    - Specifies the reduction to apply to the output:
        - none : no reduction is performed. Return NLL for each sample and for each dim separately.
        - mean : calculate mean over all samples and all dimensions.
        - sum : calculate sum over all samples and all dimensions.


**Returns:**
- picp_score: Prediction Interval Coverage Probability
- mpiw_score: Mean Prediction Interval Width

