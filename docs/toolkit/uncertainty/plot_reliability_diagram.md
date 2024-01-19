---
layout: default
title: XRAIDashboard.uncertainty.calibration.plot_reliability_diagram
parent: Uncertainty
grand_parent: Toolkit
has_children: false
nav_order: 18
---

# XRAIDashboard.uncertainty.calibration.plot_reliability_diagram
**[XRAIDashboard.uncertainty.calibration.plot_reliability_diagram(y, x, calib, n_bins = 50, reg = False, title = None, error_bars = False, error_bar_alpha = 0.05, scaling_eps = .0001, scaling_base = 10, **kwargs)](https://github.com/gaberamolete/XRAIDashboard/blob/main/uncertainty/calibration.py)**


Plots a reliability diagram of predicted vs actual probabilities.


**Parameters:**
- y (numpy.ndarray): Array or Series with ground truth labels.
- x (numpy.ndarray): Array or series of predicted values.
- calib (pd.DataFrame): Calibration object.
- n_bins (int): Number of bins used for the internal binning. Defaults to 10.
- reg (bool): Determines if y's given are from a regression or classification problem. Defaults to False.
- title (str): Title of figure. Defaults to None, and will auto-generate to "Reliability Diagram"
- error_bars (bool): Determines if error bars will be shown in the figure. Defaults to False.
- error_bar_alpha (float): The alpha value to use for error bars, based on the binomial distribution. Defaults to 0.05 (95% CI).
- scaling_eps (float): Indicates the smallest meaningful positive probability considered. Defaults to 0.0001.
- scaling_base (int): Indicates the base used when scaling back and forth. Defaults to 10.
- **kwargs: additional args to be passed to the go.Scatter plotly.graphobjects call.

**Returns:**
- fig: Plotly figure.
- area: Area between the model estimation and a hypothetical "perfect" model.

