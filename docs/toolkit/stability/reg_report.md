---
layout: default
title: XRAIDashboard.stability.stability.regression_performance_report
parent: Stability
grand_parent: Toolkit
nav_order: 1
---

# XRAIDashboard.stability.stability.regression_performance_report
**[XRAIDashboard.stability.stability.regression_performance_report(current_data, reference_data, report_format = 'json', column_mapping = None,top_error = 0.05, columns = None)](https://github.com/gaberamolete/XRAIDashboard/blob/main/stability/stability.py)**

    
For a regression model, the report shows the following:
- Calculates various regression performance metrics, including Mean Error, MAPE, MAE, etc.
- Visualizes predicted vs. actual values in a scatter plot and line plot
- Visualizes the model error (predicted - actual) and absolute percentage error in respective line plots
- Visualizes the model error distribution in a histogram
- Visualizes the quantile-quantile (Q-Q) plot to estimate value normality
- Calculates and visualizes the regression performance metrics for different groups -- top-X% with overestimation, top-X% with underestimation
- Plots relationship between feature values and model quality per group (for top-X% error groups)
- Calculates the number of instances where model returns a different output for an identical input
- Calculates the number of instances where there is a different target value/label for an identical input


**Parameters:**
- current_data: DataFrame, inference data collected after model deployment or training.
- reference_data: DataFrame, dataset used to train your initial model on.
- report_format: Specify the format to output the report object in, from `json`, `dict`, and `DataFrame`. Defaults to `json`.
- column_mapping: Input a column mapping object so the function knows how to treat each column based on data type. Defaults to None.
- top_error: Threshold for creating groups of instances with top percentiles in a) overestimation and b) underestimation. Defaults to 0.05.
- columns: List of columns to showcase in the error bias table. Defaults to None, which showcases all columns.

**Returns:**
- regression_report: Interactive visualization object containing the regression report
- rpr: Report 