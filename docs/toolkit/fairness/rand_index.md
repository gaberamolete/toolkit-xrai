---
layout: default
title: XRAIDashboard.fairness.cluster_metrics.rand_index
parent: Fairness & Performance
grand_parent: Toolkit
nav_order: 2
---

# XRAIDashboard.fairness.cluster_metrics.rand_index
**[XRAIDashboard.fairness.cluster_metrics.rand_index(num_clusters, X_train, Y_train, show = False)](https://github.com/gaberamolete/XRAIDashboard/blob/main/fairness/cluster_metrics.py)**


The Rand Index computes a similarity measure between two clusters by considering all pairs of samples and counting pairs that are assigned in the same or different clusters in the predicted and true clusterings.


**Parameters:**
- num_clusters (int): Number of clusters to be used in KMeans.
- X_train (numpy.ndarray): Training data.
- Y_train (numpy.ndarray): Training labels.
- show (bool): whether to show the plot or not

**Returns:**
- rand_dict (dict): dictionary of rand index values for each number of clusters
- fig (plotly.Figure): plotly figure of rand index vs number of clusters
