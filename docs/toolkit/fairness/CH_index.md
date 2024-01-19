---
layout: default
title: XRAIDashboard.fairness.cluster_metrics.CH_index
parent: Fairness & Performance
grand_parent: Toolkit
nav_order: 2
---

# XRAIDashboard.fairness.cluster_metrics.CH_index
**[XRAIDashboard.fairness.cluster_metrics.CH_index(num_clusters, X_train, Y_train, show = False)](https://github.com/gaberamolete/XRAIDashboard/blob/main/fairness/cluster_metrics.py)**


Calinski-Harabasz Index. The score is defined as ratio between the within-cluster dispersion and the between-cluster dispersion. The C-H Index is a great way to evaluate the performance of a Clustering algorithm as it does not require information on the ground truth labels. The higher the Index, the better the performance.


**Parameters:**
- num_clusters (int): Number of clusters to be used in KMeans.
- X_train (numpy.ndarray): Training data.
- Y_train (numpy.ndarray): Training labels.
- show (bool): whether to show the plot or not

**Returns:**
- CH_dict (dict): dictionary of CH index for each number of clusters
- fig (plotly.Figure): plotly figure of CH vs number of clusters
