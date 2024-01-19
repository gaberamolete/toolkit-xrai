---
layout: default
title: XRAIDashboard.fairness.cluster_metrics.adjusted_rand_index
parent: Fairness & Performance
grand_parent: Toolkit
nav_order: 2
---

# XRAIDashboard.fairness.cluster_metrics.adjusted_rand_index
**[XRAIDashboard.fairness.cluster_metrics.adjusted_rand_index(num_clusters, X_train, Y_train, show = False)](https://github.com/gaberamolete/XRAIDashboard/blob/main/fairness/cluster_metrics.py)**


The Rand Index but adjusted for chance. A score above 0.7 is considered a good match.


**Parameters:**
- num_clusters (int): Number of clusters to be used in KMeans.
- X_train (numpy.ndarray): Training data.
- Y_train (numpy.ndarray): Training labels.
- show (bool): whether to show the plot or not

**Returns:**
- adj_rand_dict (dict): dictionary of adjusted rand index values for each number of clusters
- fig (plotly.Figure): plotly figure of adjusted rand index vs number of clusters
