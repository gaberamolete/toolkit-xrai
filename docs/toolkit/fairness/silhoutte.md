---
layout: default
title: XRAIDashboard.fairness.cluster_metrics.silhoutte_score_visualizer
parent: Fairness & Performance
grand_parent: Toolkit
nav_order: 2
---

# XRAIDashboard.fairness.cluster_metrics.silhoutte_score_visualizer
**[XRAIDashboard.fairness.cluster_metrics.silhoutte_score_visualizer(num_clusters, X_train, Y_train)](https://github.com/gaberamolete/XRAIDashboard/blob/main/fairness/cluster_metrics.py)**


The Silhouette Coefficient is used when the ground-truth about the dataset is unknown and computes the density of clusters computed by the model. The score is computed by averaging the silhouette coefficient for each sample, computed as the difference between the average intra-cluster distance and the mean nearest-cluster distance for each sample, normalized by the maximum value. This produces a score between 1 and -1, where 1 is highly dense clusters and -1 is completely incorrect clustering.

The Silhouette Visualizer displays the silhouette coefficient for each sample on a per-cluster basis, visualizing which clusters are dense and which are not. This is particularly useful for determining cluster imbalance, or for selecting a value for 
by comparing multiple visualizers. 


**Parameters:**
- num_clusters (int): Number of clusters to be used in KMeans.
- X_train (numpy.ndarray): Training data.
- Y_train (numpy.ndarray): Training labels.

**Returns:**
- fig (plotly.Figure): silhouette_score visualisation
