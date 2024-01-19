---
layout: default
title: XRAIDashboard.fairness.cluster_metrics.db_index
parent: Fairness & Performance
grand_parent: Toolkit
nav_order: 2
---

# XRAIDashboard.fairness.cluster_metrics.db_index
**[XRAIDashboard.fairness.cluster_metrics.db_index(num_clusters, X_train, Y_train, show = False)](https://github.com/gaberamolete/XRAIDashboard/blob/main/fairness/cluster_metrics.py)**


The Davies-Bouldin Index is defined as the average similarity measure of each cluster with its most similar cluster. Similarity is the ratio of within-cluster distances to between-cluster distances. In this way, clusters which are farther apart and less dispersed will lead to a better score.

The minimum score is zero, and differently from most performance metrics, the lower values the better clustering performance.

Similarly to the Silhouette Score, the D-B Index does not require the a-priori knowledge of the ground-truth labels, but has a simpler implementation in terms of fomulation than Silhouette Score.


**Parameters:**
- num_clusters (int): Number of clusters to be used in KMeans.
- X_train (numpy.ndarray): Training data.
- Y_train (numpy.ndarray): Training labels.
- show (bool): whether to show the plot or not

**Returns:**
- DB_dict (dict): dictionary of DB index for each number of clusters
- fig (plotly.Figure): plotly figure of DBindex vs number of clusters
