---
layout: default
title: XRAIDashboard.fairness.cluster_metrics.mutual_info
parent: Fairness & Performance
grand_parent: Toolkit
nav_order: 2
---

# XRAIDashboard.fairness.cluster_metrics.mutual_info
**[XRAIDashboard.fairness.cluster_metrics.mutual_info(num_clusters, X_train, Y_train, show = False)](https://github.com/gaberamolete/XRAIDashboard/blob/main/fairness/cluster_metrics.py)**


A measure of the similarity between 2 labels of the same data. The AMI returns a value of 1 when the two partitions are identical (ie perfectly matched). Random partitions (independent labellings) have an expected AMI around 0 on average hence can be negative.



**Parameters:**
- num_clusters (int): Number of clusters to be used in KMeans.
- X_train (numpy.ndarray): Training data.
- Y_train (numpy.ndarray): Training labels.
- show (bool): whether to show the plot or not

**Returns:**
- MI_dict (dict): dictionary of mutual information for each number of clusters
- fig (plotly.Figure): plotly figure of MI vs number of clusters
