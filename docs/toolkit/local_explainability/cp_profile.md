---
layout: default
title: XRAIDashboard.local_exp.local_exp.cp_profile
parent: Local Explainability
grand_parent: Toolkit
nav_order: 1
---

# XRAIDashboard.local_exp.local_exp.cp_profile
**[XRAIDashboard.local_exp.local_exp.cp_profile(exp, obs, variables = None, var_type = 'numerical', labels = False)](https://github.com/gaberamolete/XRAIDashboard/blob/main/local_exp/local_exp.py)**


Creates a ceteris-paribus plot for a specific observation and outputs the equivalent table. User may specify the variables to showcase. Note that this can only help explain variables that are of the same data type at the same time, i.e. you may not analyze a numerical and categorical variable in the same run.


**Parameters:**
- exp: explanation object
- obs: single Dalex-enabled observation
- variables: list, list of variables to be explained utilizing the methods. The default is 'None', which will make it run through all variables.
- var_type: can either be 'numerical' or 'categorical'.
- labels: boolean. If True, will change label to 'PD profiles'.

**Returns:**
- result: DataFrame of the results from the cp_profile plot.
- plot: plotly.Figure for the visualization