---
layout: default
title: XRAIDashboard.uncertainty.calibration.calib_temp
parent: Uncertainty
grand_parent: Toolkit
has_children: false
nav_order: 3
---

# XRAIDashboard.uncertainty.calibration.calib_temp
**[XRAIDashboard.uncertainty.calibration.calib_temp(y_pred,y_true,reg)](https://github.com/gaberamolete/XRAIDashboard/blob/main/uncertainty/calibration.py)**


Temperature Scaling, a single-parameter variant of Platt Scaling.


**Parameters:**
- y_pred (numpy.ndarray): Array or series of predicted values.
- y_true (numpy.ndarray): Array or Series with ground truth labels.
- reg (bool): Determines if y's given are from a regression or classification problem. Defaults to False.

**Returns:**
- temperature: Temperature Scaling object.
- temp_calibrated: Recalibrated values under Temperature Scaling, given via array.
