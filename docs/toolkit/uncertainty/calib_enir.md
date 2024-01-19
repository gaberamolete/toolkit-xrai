---
layout: default
title: XRAIDashboard.uncertainty.calibration.calib_enir
parent: Uncertainty
grand_parent: Toolkit
has_children: false
nav_order: 7
---

# XRAIDashboard.uncertainty.calibration.calib_enir
**[XRAIDashboard.uncertainty.calibration.calib_enir(y_pred,y_true,reg)](https://github.com/gaberamolete/XRAIDashboard/blob/main/uncertainty/calibration.py)**


Ensemble of Near Isotonic Regression models (ENIR). Allows a violation of monotony restrictions. Using the modified Pool-Adjacent-Violaters Algorithm (mPAVA), this method builds multiple Near Isotonic Regression Models and weights them by a certain score function. Not recommended for regression outputs.


**Parameters:**
- y_pred (numpy.ndarray): Array or series of predicted values.
- y_true (numpy.ndarray): Array or Series with ground truth labels.
- reg (bool): Determines if y's given are from a regression or classification problem. Defaults to False.

**Returns:**
- enir: ENIR object.
- enir_calibrated: Recalibrated values under ENIR, given via array.
