---
layout: default
title: XRAIDashboard.uncertainty.uct.uct_plot_XY
parent: Uncertainty
grand_parent: Toolkit
has_children: false
nav_order: 24
---

# XRAIDashboard.uncertainty.uct.uct_plot_XY
**[XRAIDashboard.uncertainty.uct.uct_plot_XY(X_train, X_test, Y_train, Y_test, uct_data_dict, uct_metrics, column, target_feature, non_neg, show=False)](https://github.com/gaberamolete/XRAIDashboard/blob/main/uncertainty/calibration.py)**


Plot one-dimensional inputs with associated predicted values, predictive uncertainties, and true values.


**Parameters:**
- X_train (pandas.DataFrame): training dataset for X values
- X_test (pandas.DataFrame): test dataset for X values
- Y_train (pandas.DataFrame): training dataset for Y values
- Y_test (pandas.DataFrame): test dataset for Y values
- uct_data_dict (dict): dictionary of the data that is needed for the Uncertainty Toolbox
- uct_metrics (dict): Dictionary of all metrics calculated by the Uncertainty Toolbox
- column (str): x column to be plotted
- target_feature (str): name of target feature
- non_neg (bool): Boolean value whether target_feature should be non_negative
- show (bool): Boolean value to determine if the plot should be shown or not. Default to False.

**Returns:**
- fig (plotly.Figure): plotly figure of the XY plot

