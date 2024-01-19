---
layout: default
title: XRAIDashboard.local_exp.local_exp.initiate_shap_loc
parent: Local Explainability
grand_parent: Toolkit
nav_order: 1
---

# XRAIDashboard.local_exp.local_exp.initiate_shap_loc
**[XRAIDashboard.local_exp.local_exp.initiate_shap_loc(X, model, preprocessor = None, samples = 100, seed = 42, cat_cols = None)](https://github.com/gaberamolete/XRAIDashboard/blob/main/local_exp/local_exp.py)**


Initiate the shap explainer used for local explanations. Defaults to an Independent masker, but will redirect to a TabularPartitions if exceptions/errors are encountered.


**Parameters:**
- X: DataFrame, data to be modelled.
- model: model object, model used
- preprocessor: Object needed if X needs to be preprocessed (i.e. in a Pipeline) before being fed into the model. Defaults to None.
- samples: int, number of samples to be included in the TabularPartitions method. Defaults to 100.
- seed: Random state in order to ensure reproducibility. Defaults to 42.
- cat_cols: List of str, categorical variables

**Returns:**
- explainer: Shap explainer object.
- shap_values: Generated shap values, to be used for other shap-generate graphs.
- feature_names: Names of features generated from the preprocessed X DataFrame. Useful for other shap-generated graphs.