---
layout: default
title: XRAIDashboard.stability.stability.regression_performance_test
parent: Stability
grand_parent: Toolkit
nav_order: 1
---

# XRAIDashboard.stability.stability.regression_performance_test
**[XRAIDashboard.stability.stability.regression_performance_test(current_data, reference_data, test_format = 'json', column_mapping = None,approx_val = None, rel_val = 0.1)](https://github.com/gaberamolete/XRAIDashboard/blob/main/stability/stability.py)**

    
Computes the following tests on regression data, failing if +/- a percentage (%) of scores over reference data is achieved:
- Mean Absolute Error (MAE)
- Root Mean Squared Error (RMSE)
- Mean Error (ME) and tests if it is near zero
- Mean Absolute Percentage Error (MAPE)
- Absolute Maximum Error
- R2 Score (coefficient of determination)


**Parameters:**
- current_data: DataFrame, inference data collected after model deployment or training.
- reference_data: DataFrame, dataset used to train your initial model on.
- test_format: Specify the format to output the test object in, from `json`, `dict`, and `DataFrame`. Defaults to `json`.
- column_mapping: Input a column mapping object so the function knows how to treat each column based on data type. Defaults to None.
- approx_val: Dictionary, if user wants to specify values for each test. Defaults to None. See documentation for example on how to put parameters.
- rel_val: Relative percentage with which each test will pass or fail. Defaults to 0.1 (10%).

**Returns:**
- regression_test: Interactive visualization object containing the regression test
- rpt: test 