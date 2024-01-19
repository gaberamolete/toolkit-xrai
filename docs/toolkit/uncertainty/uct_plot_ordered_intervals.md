---
layout: default
title: XRAIDashboard.uncertainty.uct.uct_plot_ordered_intervals
parent: Uncertainty
grand_parent: XRAI API Documentation
has_children: false
nav_order: 23
permalink: /docs/toolkit/api_documentation/uncertainty
---

# XRAIDashboard.uncertainty.uct.uct_plot_ordered_intervals
**[XRAIDashboard.uncertainty.uct.uct_plot_ordered_intervals(X_train, X_test, Y_train, Y_test, uct_data_dict, uct_metrics, non_neg, show=False)](https://github.com/gaberamolete/XRAIDashboard/blob/main/uncertainty/calibration.py)**


Plot predictions and predictive intervals versus true values, with points ordered by true value along x-axis.


**Parameters:**
- X_train (pandas.DataFrame): training dataset for X values
- X_test (pandas.DataFrame): test dataset for X values
- Y_train (pandas.DataFrame): training dataset for Y values
- Y_test (pandas.DataFrame): test dataset for Y values
- uct_data_dict (dict): dictionary of the data that is needed for the Uncertainty Toolbox
- uct_metrics (dict): Dictionary of all metrics calculated by the Uncertainty Toolbox
- non_neg (bool): Boolean value whether target_feature should be non_negative
- show (bool): Boolean value to determine if the plot should be shown or not. Default to False.

**Returns:**
- fig (plotly.Figure): plotly figure of the ordered intervals

