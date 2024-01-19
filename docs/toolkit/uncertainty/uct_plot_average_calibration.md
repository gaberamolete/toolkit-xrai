---
layout: default
title: XRAIDashboard.uncertainty.uct.uct_plot_average_calibration
parent: Uncertainty
grand_parent: Toolkit
has_children: false
nav_order: 22
---

# XRAIDashboard.uncertainty.uct.uct_plot_average_calibration
**[XRAIDashboard.uncertainty.uct.uct_plot_average_calibration(uct_data_dict, uct_metrics, show = False)](https://github.com/gaberamolete/XRAIDashboard/blob/main/uncertainty/calibration.py)**


Plot the observed proportion vs prediction proportion of outputs falling into a range of intervals, and display miscalibration area.


**Parameters:**
- uct_data_dict (dict): dictionary of the data that is needed for the Uncertainty Toolbox
- uct_metrics (dict): Dictionary of all metrics calculated by the Uncertainty Toolbox
- show (bool): Boolean value to determine if the plot should be shown or not. Default to False.

**Returns:**
- fig (plotly.Figure): plotly figure of the average calibration

