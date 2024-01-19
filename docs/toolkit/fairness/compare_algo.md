---
layout: default
title: XRAIDashboard.fairness.fairness_algorithm.compare_algorithms
parent: Fairness & Performance
grand_parent: Toolkit
nav_order: 4
---

# XRAIDashboard.fairness.fairness_algorithm.compare_algorithms
**[XRAIDashboard.fairness.fairness_algorithm.compare_algorithms(b, di, rw, egr, mc, ceo, ro, threshold, metric_name="Disparate impact")](https://github.com/gaberamolete/XRAIDashboard/blob/main/fairness/fairness_algorithm.py)**


Produce a scatter plot to compare the effectiveness of each algorithm to a specific metric, and also observe the fairness vs. performance trade-off


**Parameters:**
- b (OrderedDict): containts the fairness scores of the model before any algorithm
- di (OrderedDict): contains the fairness scores of the model after the disparate impact remover algorithm
- rw (OrderedDict): contains the fairness scores of the model after the reweighing algorithm
- egr (OrderedDict): contains the fairness scores of the model after the exponentiated gradient reduction algorithm
- mc (OrderedDict): contains the fairness scores of the model after the meta-classifier algorithm
- ceo (OrderedDict): contains the fairness scores of the model after the calibratied equalized odds algorithm
- ro (OrderedDict): contains the fairness scores of the model after the reject option algorithm
- metric_name (str): the fairness metric to analyze

**Returns:**
None

*Note: This shows the comparison visualization*