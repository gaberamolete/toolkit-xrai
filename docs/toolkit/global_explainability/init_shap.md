---
layout: default
title: XRAIDashboard.global_exp.global_exp.initiate_shap_glob
parent: Global Explainability
grand_parent: Toolkit
nav_order: 1
---

# XRAIDashboard.global_exp.global_exp.initiate_shap_glob
**[XRAIDashboard.global_exp.global_exp.initiate_shap_glob(X, model, preprocessor = None, samples = 100, seed = 42, cat_cols = None)](https://github.com/gaberamolete/XRAIDashboard/blob/main/global_exp/global_exp.py)**


Initiate instance for SHAP global object. Defaults to a TreeExplainer, but will redirect to a KernelExplainer if exceptions/errors are encountered.


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