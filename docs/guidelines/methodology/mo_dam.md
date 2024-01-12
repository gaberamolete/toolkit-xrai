---
layout: default
title: M&O - Determining Applicable Methodology
parent: XRAI Methodology
grand_parent: Guidelines
nav_order: 2
---

# XRAI Methodology - Model & Output (M&O) - Determining Applicable Methodology
{: .no_toc }

<!-- ## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc} -->

The XRAI Guidelines provide recommendations for specific scenarios. Taking these steps will allow users to deal with these common Data Science problems while also adhering to the XRAI principles. The list below is not exhaustive, but provides a reference point of incorporating the XRAI principles to the Data Science development process.  

1. Data Preprocessing  
- **Handle Missing Data**: Decide on a strategy for handling missing values (e.g., impute with mean, median, or a custom value). Document your approach and make sure it doesn't introduce bias or distort the data. 
- **Remove Duplicates**: Identify and remove duplicate records if they exist. 
- **Outlier Detection and Treatment**: Identify outliers using statistical methods or visualizations.  Decide whether to remove, transform, or leave outliers as is based on domain knowledge. 
- **Data Type Conversion**: Ensure data types are appropriate for analysis (e.g., converting text labels to numerical values). 

{:style="counter-reset:none"}
1. Feature Engineering  
- **Categorical Encoding**: Use appropriate encoding techniques for categorical features to convert them into numerical representations. Common methods include one-hot encoding, label encoding, or target encoding. Choose encoding methods that align with model interpretability requirements. 
- **Feature Scaling and Normalisation**: Scaling features to a common range (e.g., [0, 1] or standardized with mean 0 and variance 1) can help models perform better and make their explanations more interpretable. Scaling ensures that all features contribute to the model on an equal footing. 
- **Feature Selection**: Reduce the number of features by selecting the most important features. Techniques like feature importance from tree-based models or feature selection algorithms (e.g., Recursive Feature Elimination) can be useful. Feature selection can enhance model interpretability by focusing on the most relevant variables. 
- **Principal Component Analysis**: Use PCA for dimensionality reduction when dealing with high-dimensional data. PCA can help uncover the underlying structure in data while reducing complexity.  Visualize the first few principal components to understand which original features contribute most to them. 
- **XRAI Techniques**: Document all feature engineering steps and rationale behind these steps. Utilize SHAP values or partial dependence plots, to explain how individual features impact model predictions. Visualize feature importance to provide insights into which features are most influential in the model's decision-making process. 