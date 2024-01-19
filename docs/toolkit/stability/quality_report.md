---
layout: default
title: XRAIDashboard.stability.stability.data_quality_dataset_report
parent: Stability
grand_parent: Toolkit
nav_order: 1
---

# XRAIDashboard.stability.stability.data_quality_dataset_report
**[XRAIDashboard.stability.stability.data_quality_dataset_report(current_data, reference_data, report_format = 'json', column_mapping = None,adt = 0.95, act = 0.95):](https://github.com/gaberamolete/XRAIDashboard/blob/main/stability/stability.py)**


Calculate various descriptive statistics, the number and share of missing values per column, and correlations between columns in the dataset.


**Parameters:**
- current_data: DataFrame, inference data collected after model deployment or training.
- reference_data: DataFrame, dataset used to train your initial model on.
- report_format: Specify the format to output the report object in, from `json`, `dict`, and `DataFrame`. Defaults to `json`.
- column_mapping: Input a column mapping object so the function knows how to treat each column based on data type.
- adt: Almost Duplicated Threshold, for when values look to be very similar to each other. Defaults to 0.95.
- act: Almost Constant Threshold, for when a column exhibits almost no variance. Defaults to 0.95.

**Returns:**
- data_quality_report: Interactive visualization object containing the data quality report
- dqr: Report 