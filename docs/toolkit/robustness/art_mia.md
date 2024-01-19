---
layout: default
title: XRAIDashboard.robustness.art_mia.art_mia
parent: Robustness
grand_parent: Toolkit
nav_order: 1
---

# XRAIDashboard.robustness.art_mia.art_mia
**[XRAIDashboard.robustness.art_mia.art_mia(x_train, y_train, x_test, y_test, art_extra_dict, key, attack_train_ratio=0.3)](https://github.com/gaberamolete/XRAIDashboard/blob/main/robustness/art_mia.py)**

    
Returns the inferred train and inferred test 


**Parameters:**
- x_train : numpy array
- y_train : numpy array
- x_test : numpy array
- y_test : numpy array
- art_extra_dict : dictionary of ART and extra models

**Returns:**
- inferred_train: array like train set for inference from the attacking model
- inferred_test: array like test set for inference from the attacking model