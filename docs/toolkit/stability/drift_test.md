---
layout: default
title: XRAIDashboard.stability.stability.data_drift_dataset_test
parent: Stability
grand_parent: Toolkit
nav_order: 1
---

# XRAIDashboard.stability.stability.data_drift_dataset_test
**[XRAIDashboard.stability.stability.data_drift_dataset_test(current_data, reference_data, test_format = 'json', column_mapping = None, = 0.5, stattest = None, stattest_threshold = None, cat_stattest = None, cat_stattest_threshold = None, num_stattest = None, num_stattest_threshold = None, per_column_stattest = None, per_column_stattest_threshold = None):](https://github.com/gaberamolete/XRAIDashboard/blob/main/stability/stability.py)**


This compares the distribution of each column in the current dataset to the reference and tests the number and share of drifting features against a defined condition.
    
Drift detection methods that can be used for `stattest` and other equivalent parameters are as follows:
- `ks`: Kolmogorov-Smirnov test, only numerical. Returns p_value drift detected when less than threshold (default is 0.05).
- `chisquare`: Chi-Square test, only categorical. Returns p_value drift detected when less than threshold (default is 0.05).
- `z`: Z-test, only categorical. Returns p_value drift detected when less than threshold (default is 0.05).
- `wasserstein`: Normalized Wasserstein distance, only numerical. Returns distance drift detected when greater than or equal to threshold (default is 0.1).
- `kl_div`: Kullback-Leibler, numerical and categorical. Returns divergence drift detected when greater than or equal to threshold (default is 0.1).
- `psi`: Population Stability Index, numerical and categorical. Returns psi_value drift detected when greater than or equal to threshold (default is 0.1).
- `jensenshannon`: Jensen-Shannon distance, numerical and categorical. Default method for categorical, if there are > 1000 objects. Returns distance drift detected when greater than or equal to threshold (default is 0.1).
- `anderson`: Anderson-Darling test, only numerical. Returns p_value drift detected when less than threshold (default is 0.05).
- `fisher_exact`: Fisher's Exact test, only categorical. Returns p_value drift detected when less than threshold (default is 0.05).
- `cramer_von_mises`: Cramer-Von-Mises test, only numerical. Returns p_value drift detected when less than threshold (default is 0.05).
- `g-test`: G-test, only categorical. Returns p_value drift detected when less than threshold (default is 0.05).
- `hellinger`: Normalized Hellinger distance, numerical and categorical. Returns distance drift detected when greater than or equal to threshold (default is 0.1).
- `mannw`: Mann-Whitney U-rank test, only numerical. Returns p_value drift detected when less than threshold (default is 0.05).
- `ed`: Energy distance, only numerical. Returns distance drift detected when greater than or equal to threshold (default is 0.1).
- `es`: Epps-Singleton tes, only numerical. Returns p_value drift detected when less than threshold (default is 0.05).
- `t_test`: T-Test, only numerical. Returns p_value drift detected when less than threshold (default is 0.05).
- `emperical_mmd`: Emperical-MMD, only numerical. Returns p_value drift detected when less than threshold (default is 0.05).
- `TVD`: Total-Variation-Distance, only categorical. Returns p_value drift detected when less than threshold (default is 0.05).
A combination of these tests are used if `stattest` and other equivalent parameters are not explicitly specified.


**Parameters:**
- current_data: DataFrame, inference data collected after model deployment or training.
- reference_data: DataFrame, dataset used to train your initial model on.
- test_format: Specify the format to output the test object in, from `json`, `dict`, and `DataFrame`. Defaults to `json`.
- column_mapping: Input a column mapping object so the function knows how to treat each column based on data type.
- drift_share: Threshold to determine when dataset achieves data drift. Calculated by dividing the number of columns with detected data drift over all total columns. Defaults to 0.5.
- stattest: Defines the drift detection method for a given column (if a single column is tested), or all columns in the dataset (if multiple columns are tested).
- stattest_threshold: Sets the drift threshold in a given column or all columns. The threshold meaning varies based on the drift detection method, e.g., it can be the value of a distance metric or a p-value of a statistical test.
- cat_stattest: Sets the drift method for all categorical columns in the dataset.
- cat_stattest_threshold: Sets the threshold for all categorical columns in the dataset.
- num_stattest: Sets the drift method for all numerical columns in the dataset.
- num_stattest_threshold: Sets the threshold for all numerical columns in the dataset.
- per_column_stattest: Sets the drift method for the listed columns (accepts a dictionary).
- per_column_stattest_threshold: Sets the threshold for the listed columns (accepts a dictionary).

**Returns:**
- data_drift_test: Interactive visualization object containing the data drift test
- ddt: test results