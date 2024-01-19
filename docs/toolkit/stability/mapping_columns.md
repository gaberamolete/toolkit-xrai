---
layout: default
title: XRAIDashboard.stability.stability.mapping_columns
parent: Stability
grand_parent: Toolkit
nav_order: 1
---

# XRAIDashboard.stability.stability.mapping_columns
**[XRAIDashboard.stability.stability.mapping_columns(current_data, reference_data, model, target, prediction = None, id_cols = None, datetime_cols = None, num_cols = None, cat_cols = None)](https://github.com/gaberamolete/XRAIDashboard/blob/main/stability/stability.py)**


Mapping column types for other Evidently-based functions.


**Parameters:**
- current_data: DataFrame, inference data collected after model deployment or training.
- reference_data: DataFrame, dataset used to train your initial model on.
- model: Model used to train data.
- target: str, name of the target column in both the `current_data` and `reference_data`.
- prediction: str, name of the prediction column in both the `current_data` and `reference_data`. Defaults to None.
- id_cols: List of ID columns found in the data. Defaults to None.
- datetime_cols: List of datetime columns found in the data. Defaults to None.
- num_cols: List of numerical columns found in the data. Defaults to None.
- cat_cols: List of categorical columns found in the data. Defaults to None.

**Returns:**
- current_data: DataFrame, inference data collected after model deployment or training.
- reference_data: DataFrame, dataset used to train your initial model on.
- column_mapping: Object that tells other functions how to treat each column based on data type.