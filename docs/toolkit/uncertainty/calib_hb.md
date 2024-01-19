---
layout: default
title: XRAIDashboard.uncertainty.calibration.calib_hb
parent: Uncertainty
grand_parent: Toolkit
has_children: false
nav_order: 4
---

# XRAIDashboard.uncertainty.calibration.calib_hb
**[XRAIDashboard.uncertainty.calibration.calib_hb(y_pred,y_true,reg)](https://github.com/gaberamolete/XRAIDashboard/blob/main/uncertainty/calibration.py)**


Histogram binning, where each prediction is sorted into a bin and assigned a calibrated confidence estimate.


**Parameters:**
- y_pred (numpy.ndarray): Array or series of predicted values.
- y_true (numpy.ndarray): Array or Series with ground truth labels.
- reg (bool): Determines if y's given are from a regression or classification problem. Defaults to False.

**Returns:**
- hb: Histogram Binning object.
- hb_calibrated: Recalibrated values under Histogram Binning, given via array.
