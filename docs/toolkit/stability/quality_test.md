---
layout: default
title: XRAIDashboard.stability.stability.data_quality_dataset_test
parent: Stability
grand_parent: Toolkit
nav_order: 1
---

# XRAIDashboard.stability.stability.data_quality_dataset_test
**[XRAIDashboard.stability.stability.data_quality_dataset_test(current_data, reference_data, test_format = 'json', column_mapping = None,adt = 0.95, act = 0.95):](https://github.com/gaberamolete/XRAIDashboard/blob/main/stability/stability.py)**


For all columns in a dataset:
- Tests number of rows and columns against reference or defined condition
- Tests number and share of missing values in the dataset against reference or defined condition
- Tests number and share of columns and rows with missing values against reference or defined condition
- Tests number of differently encoded missing values in the dataset against reference or defined condition
- Tests number of columns with all constant values against reference or defined condition
- Tests number of empty rows (expects 10% or none) and columns (expects none) against reference or defined condition
- Tests number of duplicated rows (expects 10% or none) and columns (expects none) against reference or defined condition
- Tests types of all columns against the reference, expecting types to match


**Parameters:**
- current_data: DataFrame, inference data collected after model deployment or training.
- reference_data: DataFrame, dataset used to train your initial model on.
- test_format: Specify the format to output the test object in, from `json`, `dict`, and `DataFrame`. Defaults to `json`.
- column_mapping: Input a column mapping object so the function knows how to treat each column based on data type.

**Returns:**
- data_quality_test: Interactive visualization object containing the data quality test
- dqr: Test results