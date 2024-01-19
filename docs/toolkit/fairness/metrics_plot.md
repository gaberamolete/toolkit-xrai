---
layout: default
title: XRAIDashboard.fairness.fairness_algorithm.metrics_plot
parent: Fairness & Performance
grand_parent: Toolkit
nav_order: 4
---

# XRAIDashboard.fairness.fairness_algorithm.metrics_plot
**[XRAIDashboard.fairness.fairness_algorithm.metrics_plot(metrics1, threshold, metric_name, protected, metrics2=None)](https://github.com/gaberamolete/XRAIDashboard/blob/main/fairness/fairness_algorithm.py)**


Plot the score of a specific fairness metric in a horizontal bar plot. Green region signifies the acceptable values where the model is fair, while the red region signifies that model is not fair. The area of these region is set on based on the threshold value. If a second set of metrics is inputted, the plot will be a grouped horizontal bar plot.


**Parameters:**
-  metrics1 (OrderedDict): Contains the fairness scores of the model
- threshold (float): How far from the ideal value is the acceptable range for the fairness metric
- metric_name (str): The fairness metric to analyze, must be a key from metrics1
- protected (str): The protected group to analyze fairness with
- metrics2 (OrderedDict, optional): A second set of metric scores for comparison. Default is None.

**Returns:**
- fig (plotly.Figure): Visualization of the chosen metric.