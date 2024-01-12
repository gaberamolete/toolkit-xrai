---
layout: default
title: M&O - Explainability
parent: XRAI Methodology
grand_parent: Guidelines
nav_order: 6
---

# XRAI Methodology - Model & Output (M&O) - Explainability
{: .no_toc }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

Explainability is to the ability to **understand and interpret how a machine learning model makes its predictions or decisions**. It's a critical aspect of machine learning, especially in applications where the consequences of a model's decisions are important. Explainability helps users, stakeholders, and regulators gain trust in the model and ensure it's making decisions for the right reasons, avoiding bias, and following ethical guidelines. 

## Types of Explainability
There are two main types of explainability in machine learning: 

1. Global Explainability 
- Global explainability focuses on understanding the overall behavior of a machine learning model. It aims to provide insights into how the model is learning from the entire dataset and the relative importance of different features. 
- Common techniques for global explainability include:
    - **Feature importance scores**, which rank the importance of input features in making predictions 
    - **Partial Dependence Plots (PDPs)**, which show how the predicted outcome of a model changes if a single input feature varies 
    - **Accumulated Local Effects (ALE) plots**, which capture non-linear relationships between features and predictions 
    - **Feature Correlation Analysis**, which can help identify multicollinearity among features, affecting a model’s interpretability 
- Global explainability methods are useful for getting a high-level understanding of which features are most influential in the model's predictions. 

2. Local Explainability
- Local explainability focuses on understanding individual predictions made by the machine learning model. It aims to provide insights into why a specific prediction was made for a particular input instance. 
- Common techniques for local explainability include 
    - **LIME (Local Interpretable Model-Agnostic Explanations)**, which generates local explanations by training a simpler, interpretable model on a smaller subset of data based on nearby points 
    - **Integrated Gradients**, which computes the integral of gradients along the path from a baseline input (reference) to the target input instance 
    - **Attention maps** (for neural networks), which can be used to visualize which parts of the input the model focused on when making a prediction 
    - **Counterfactual explanations**, which show how small changes in input would lead to a different outcome 
- Local explainability methods aim to create interpretable explanations for a single prediction, such as highlighting the importance of specific features or showing how the input features contributed to the output. This can help users understand the model's reasoning on a case-by-case basis. 

There are plenty of libraries and modules available which support the creation of local and global explainability functions. Here are some below: 

## DiCE 
[DICE Diverse Counterfactual Explanations (DiCE)](https://github.com/interpretml/DiCE) is a tool developed by Microsoft that provides counterfactual explanations for machine learning models. Counterfactual explanations are a type of explanation that can help users understand why a machine learning model made a particular prediction or decision. They do this by showing what changes would need to be made to the input features of a model in order to change its output. 

## Quantitative Input Influence 
[Quantitative Input Influence (QII)](https://www.andrew.cmu.edu/user/danupam/datta-sen-zick-oakland16.pdf) is a method for quantifying the impact of each input feature on the model's output. QII can be used to identify which input features are most important to the model's decision, and how changes to those features would impact the output. 

## SHAP  
[SHAP](https://shap.readthedocs.io/en/latest/), which stands for SHapley Additive exPlanations, is a method used in machine learning and data analysis for explaining the output of complex predictive models. It provides a way to interpret the contributions of individual features or variables to the predictions made by a model. SHAP values are based on cooperative game theory and the concept of Shapley values, which were originally developed to fairly distribute payouts among participants in a cooperative game. 

In the context of machine learning, SHAP values offer a way to allocate the contribution of each feature to the difference between a model's prediction and a baseline prediction. They provide a local explanation for a specific prediction, indicating how much each feature pushed the prediction away from the baseline. 

There are various methods to compute SHAP values for different types of models, including tree-based models, linear models, and deep learning models. The core idea remains consistent: to attribute the difference in prediction to each feature in a fair and consistent manner. Here are some different methods and techniques you can use with SHAP: 

1. **SHAP Values Calculation**: The core concept of SHAP is to compute SHAP values, which quantify the impact of each feature on a specific prediction compared to a baseline prediction. You can calculate SHAP values using various algorithms tailored to different types of models, such as tree-based models, linear models, and deep learning models. 
2. **Visualizing Individual Explanations**: Use SHAP values to create visualizations that explain the prediction for a single instance. SHAP summary plots show how each feature contributes to the prediction for that instance, making it easier to understand the factors influencing the outcome. 
3. **Feature Importance Ranking**: SHAP values provide a principled way to rank features based on their contributions to model predictions. You can use SHAP values to create sorted bar charts or summary plots to visualize feature importance. 
4. **Global Feature Importance**: Analyze the global importance of features across all instances in the dataset. Aggregating SHAP values across instances can give you insights into which features have the most consistent impact on predictions across the entire dataset. 
5. **Interaction Effects Analysis**: SHAP values allow you to investigate interactions between features. By analyzing how SHAP values change as features vary together, you can understand how feature interactions affect predictions. 
6. **Model Debugging**: Use SHAP values to identify instances where the model's predictions are unexpected or incorrect. By examining the contributions of individual features, you can pinpoint the reasons behind model errors and take corrective actions. 
7. **Partial Dependence Plots (PDPs)**: Combine SHAP values with partial dependence plots to visualize how changing a feature's value influences the model's prediction. PDPs show the average prediction trend while SHAP values provide insights into individual prediction variations. 
8. **Group Feature Contributions**: For categorical features, you can visualize the contributions of individual categories within the feature. This is particularly useful for understanding how different categories impact predictions. 
9. **Model Explanation Comparison**: Compare the explanations generated by SHAP values between different models or model versions. This can help you understand why models behave differently and identify improvements. 
10. **Fairness and Bias Analysis**: Apply SHAP values to assess the fairness and potential bias of a model's predictions. By examining how SHAP values vary across different demographic groups, you can identify areas where biases might exist. 
11. **Dimensionality Reduction**: SHAP values can be used to reduce high-dimensional data to a lower-dimensional representation while preserving the interpretability of feature contributions. 
12. **Ensemble Model Interpretation**: SHAP values can be applied to ensemble models to explain their predictions. You can analyze how contributions from individual base models combine to form the ensemble's predictions. 

SHAP provides a comprehensive framework for model interpretation and understanding, and its applications are broad and powerful. Depending on your specific goals, dataset, and model type, you can leverage SHAP values for various techniques to gain insights and transparency into complex machine learning models. 

## Other techniques
Aside from what was previously mentioned, here are other explainability tools and methods: 
- Model-specific tools/libraries: 
    - [Explain Like I’m Five](https://eli5.readthedocs.io/en/latest/overview.html) (ELI5) (sklearn regressors and classifiers, XGBoost, CatBoost, LightGBM, Keras) 
    - [Activation Atlases](https://distill.pub/2019/activation-atlas/) (for [neural networks](https://github.com/tensorflow/lucid)) 
    - [What-if Tool](https://github.com/PAIR-code/what-if-tool) (WIT) (TensorFlow models, XGBoost and Scikit-Learn models). 
- Model-agnostic tools/libraries: 
    - [skater](https://github.com/GapData/skater) (deep neural networks, tree algorithms, and scalable Bayes) 
    - [InterpretML](https://interpret.ml/) (LIME, SHAP, linear models, and decision tree) 
    - [Alibi Explain](https://docs.seldon.io/projects/alibi/en/latest/), used for model inspection and interpretation of black-box and glass-box models, both via local and global explanation methods 
    - [Rulex Explainable AI](https://www.rulex.ai/) (Logic learning machine) 
    - [Model Agnostic Language for Exploration and Explanation](https://dalex.drwhy.ai/) (DALEX) (XGBoost, TensorFlow, h2o). 
- Other explainability techniques: 
    - **Feature importance analysis/techniques** – This aims at generating a feature score that is directly proportional to the feature’s effect on the overall predictive quality of the model. Examples: mean decrease impurity (MDI), mean decrease accuracy (MDA), single feature importance (SFI). 
    - **Force dependence plots** – This presents a scatter plot that shows the effect of a single feature on model predictions. 
    - **Baselines and counterfactuals** – These techniques select a baseline that introduces the concept of a baseline score (to compare against). 
    - **Causal inferences** – This technique tests the causal relationships based on model outcomes.  