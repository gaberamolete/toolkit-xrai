---
layout: default
title: XRAIDashboard.fairness.outlier.outlier
parent: Fairness & Performance
grand_parent: Toolkit
nav_order: 3
---

# XRAIDashboard.fairness.outlier.outlier
**[XRAIDashboard.fairness.outlier.outlier(train,test,methods=[KNN,IForest],contamination=0.05)](https://github.com/gaberamolete/XRAIDashboard/blob/main/fairness/outlier.py)**


Detects outliers and remove them if user wants. We recomend first to do missing value treatment then feed your datasets into this model.


**Parameters:**
- train (pandas.DataFrame): The data set that outlier analysis is going to be done on it. we train detectors on this data set,
- test (pandas.DataFrame): Data set that you would like to do predection on it
- method (List(str)): Outlier detection method name options to choose from:
    - ABOD: Angle-based Outlier Detector ,
    - CBLOF:Clustering Based Local Outlier Factor,
    - ALAD: Adversarially Learned Anomaly Detection,
    - ECOD:Unsupervised Outlier Detection Using Empirical Cumulative Distribution Functions (ECOD),
    - IForest:IsolationForest Outlier Detector. Implemented on scikit-learn library,
    - AnoGAN: Anomaly Detection with Generative Adversarial Networks,
    - KNN:k-Nearest Neighbors Detector,
    - KPCA: Kernel Principal Component Analysis (KPCA) Outlier Detector,
    - XGBOD:Improving Supervised Outlier Detection with Unsupervised Representation Learning. A semi-supervised outlier detection framework.
    - PCA: Principal Component Analysis (PCA) Outlier Detector
- contamination (float): Amount of detected outlier by the method, range is (0-1), the higher the value the stricter the method

**Returns:**
- Labels_train (pandas.DataFrame): Data required for visualization
- Labels_test (pandas.DataFrame): Data required for visualization
