---
layout: default
title: XRAIDashboard.stability.stability.data_quality_column_test
parent: Stability
grand_parent: Toolkit
nav_order: 1
---

# XRAIDashboard.stability.stability.data_quality_column_test
**[XRAIDashboard.stability.stability.data_quality_column_test(current_data, reference_data, column, test_format = 'json', n_sigmas = 2, quantile = 0.75):](https://github.com/gaberamolete/XRAIDashboard/blob/main/stability/stability.py)**


For a given column in the dataset:
- Tests number and share of missing values in a given column against reference or defined condition
- Tests number of differently encoded missing values in a given column against reference or defined condition
- Tests if all values in a given column are a) constant, b) unique
- Tests the minimum and maximum value of a numerical column against reference or defined condition
- Tests the mean, median, and standard deviation of a numerical column against reference or defined condition
- Tests the number and share of unique values against reference or defined condition
- Tests the most common value in a categorical column against reference or defined condition
- Tests if the mean value in a numerical column is within expected range, defined in standard deviations
- Tests if numerical column contains values out of min-max range, and its share against reference or defined condition
- Tests if a categorical variable contains values out of the list, and its share against reference or defined condition
- Computes a quantile value and compares to reference or defined condition
    


**Parameters:**
- current_data: DataFrame, inference data collected after model deployment or training.
- reference_data: DataFrame, dataset used to train your initial model on.
- column: Column from both current and reference data to detect drift on.
- test_format: Specify the format to output the test object in, from `json`, `dict`, and `DataFrame`. Defaults to `json`.
- n_sigmas: # of sigmas (standard deviations) to test on mean value of a numerical column. Defaults to 2.
- quantile: Float, from [0, 1] to showcase quantile value in distribution. Defaults to 0.75.
    

**Returns:**
- data_quality_test: Interactive visualization object containing the data quality test
- dqr: test results 