---
layout: default
title: XRAIDashboard.stability.stability.data_quality_column_report
parent: Stability
grand_parent: Toolkit
nav_order: 1
---

# XRAIDashboard.stability.stability.data_quality_column_report
**[XRAIDashboard.stability.stability.data_quality_column_report(current_data, reference_data, column, report_format = 'json', quantile = 0.75,  values_list = None):](https://github.com/gaberamolete/XRAIDashboard/blob/main/stability/stability.py)**


For an identified column:
- Calculates various descriptive statistics,
- Calculates number and share of missing values
- Plots distribution histogram,
- Calculates quantile value and plots distribution,
- Calculates correlation between defined column and all other columns
- If categorical, calculates number of values in list / out of the list / not found in defined column
- If numerical, calculates number and share of values in specified range / out of range in defined column, and plots distributions
    


**Parameters:**
- current_data: DataFrame, inference data collected after model deployment or training.
- reference_data: DataFrame, dataset used to train your initial model on.
- column: Column from both current and reference data to detect drift on.
- report_format: Specify the format to output the report object in, from `json`, `dict`, and `DataFrame`. Defaults to `json`.
- quantile: Float, from [0, 1] to showcase quantile value in distribution. Defaults to 0.75.
- values_list: List of values to showcase for either a range (numerical, e.g. [10, 20] for an `Age` column) or list (categorical, e.g. ['High School', 'Post-Graduate'] for an `Education` column). Defaults to None.
    

**Returns:**
- data_quality_report: Interactive visualization object containing the data quality report
- dqr: Report 