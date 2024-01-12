---
layout: default
title: Deployment & Monitoring (D&M)
parent: XRAI Methodology
grand_parent: Guidelines
nav_order: 9
---

# XRAI Methodology - Deployment & Monitoring (D&M)
{: .no_toc }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

## Check for model drift  
Model drift is the reduction in a model’s predictive capability due to changes in the external environments. Model drift could be caused by many reasons, which include changes in the technological environment and the consequential changes in relationship between variables. Model drift can be broadly classified into two categories: data drift and concept drift.  

Some methods can be used to inspect for model drift. The Kolmogorov-Smirnov test (KS test) which is a nonparametric test, compares the training and post-training data. If the KS test states that the data distributions from both datasets are different, this will confirm the presence of model drift. The population stability Index (PSI) compares the distribution of the target feature in the test dataset with the training dataset used to develop the model. The other method for drift detection is Page-Hinkley Test by calculating the mean of the observed value and updating the mean when a new data is injected. The drift will be presence when the mean value is greater than the threshold value lambda. Another method, the adaptive Windowing (ADWIN) algorithm adopts a sliding window approach to detect model drift. ADWIN slides a fixed-size window to detect any changes in the new data, and an alert is set, if the changes exceed a pre-set threshold. 

## Check for data drift 
Data drift refers to changes in the distribution of the input features, while the relationship between the features and the target variable remains the same. This means that the statistical properties of the input features change over time, but the underlying concept or meaning of the data remains the same. For example, in a customer churn prediction system, the distribution of customer demographics or transaction data may change over time, leading to a change in the statistical properties of the input features. This can cause the model to become less accurate and may require the model to be retrained or adapted to the new data.  

Data drift can happen when there is a significant gap between the time the data is collected and when the model is used to predict outcomes using real-time data. If this problem is not addressed in a timely manner, this will negatively impact business decisions that were reliant on the model’s predictive capabilities. 

One of the common practices in catching data drifts is by using out-of-time (OOT) testing. OOT testing is the process of testing the model using unforeseen data and inspecting the model’s performance (ie., any decrease in the predictive model performance). A suggested threshold for data drift and retraining is if model performance decreases by more than 15%. However, this threshold value can be selected based on each Data Science team and use case. Furthermore, the Population Stability Index (PSI) or the Characteristics Stability Index (CSI) can be used to quantify the magnitude of the data drift, and these indices can be communicated to the business team that retraining of the model may be required. 

## Check for concept drift  
Concept drift refers to changes in the relationship between the input features and the target variable. This means that the underlying concept or meaning of the data changes over time. For example, in a fraud detection system, the types of frauds that are being committed may change over time, leading to a change in the underlying relationship between the features and the target variable. As a result, the model trained on the initial data may become less accurate over time and may need to be retrained or adapted to the new data.  

The same bias metrics during modelling can be used to inspect concept drift. Inspections can be set at frequency selected based on Data Science team and use case (e.g. DDPL bias can be computed every two days, and alert is set if bias metric exceeds confidence interval). 