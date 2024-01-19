---
layout: default
title: XRAIDashboard.local_exp.local_exp.breakdown
parent: Local Explainability
grand_parent: Toolkit
nav_order: 1
---

# XRAIDashboard.local_exp.local_exp.breakdown
**[XRAIDashboard.local_exp.local_exp.breakdown(exp, obs, order = None, random_state = 42, N = None, labels = None)](https://github.com/gaberamolete/XRAIDashboard/blob/main/local_exp/local_exp.py)**


The plot presents variable attribution to model performance by highlighting the importance of order. The default function preselects variable order based on local accuracy. Users can also select their own variable order with `order`.


**Parameters:**
- exp: explanation object
- obs: single Dalex-enabled observation
- order: order of variables to be input to the function. Defaults to None.
- random_state: defines the random state in which the number of observations to be sampled. Defaults to 42 for reproducibility.
- N: Number of observations to be sampled with. Defaults to None. Writing an int will have the function use N observations of data expensive.
- labels: label attached to the plot. Defaults to None.

**Returns:**
- result: DataFrame of the results from the break down plot.
- plot: plotly.Figure for the visualization