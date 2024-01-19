---
layout: default
title: XRAIDashboard.local_exp.local_exp.interactive
parent: Local Explainability
grand_parent: Toolkit
nav_order: 1
---

# XRAIDashboard.local_exp.local_exp.interactive
**[XRAIDashboard.local_exp.local_exp.interactive(exp, obs, count = 10, random_state = 42, N = None, labels = None)](https://github.com/gaberamolete/XRAIDashboard/blob/main/local_exp/local_exp.py)**


Adds interactions to the usual break-down plot.


**Parameters:**
- exp: explanation object
- obs: single Dalex-enabled observation- count: number of new 'interaction' variables to be made. Defaults to 10 to keep it relatively computationally inexpensive.
- random_state: defines the random state in which the number of observations to be sampled. Defaults to 42 for reproducibility.
- N: Number of observations to be sampled with. Defaults to None. Writing an int will have the function use N observations of data expensive.
- labels: label attached to the plot. Defaults to None.

**Returns:**
- result: DataFrame of the results from the interactive plot.
- plot: plotly.Figure for the visualization