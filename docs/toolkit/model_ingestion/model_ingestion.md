---
layout: default
title: Model Ingestion
parent: Toolkit
nav_order: 1
has_children: True
permalink: /docs/toolkit/model_ingestion
---

# Model Ingestion
{: .no_toc }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

## Data Preparations

Import the function from the XRAI package.


```python
from XRAIDashboard.model_ingestion.data_model import load_data_model
```


The `load_data_model` function requires the file path of the train and test csv files, the models, and the target variable in the data. Set up the file path of the train and test csv files in a variable. For the models, collect all the file_path in a dictionary form, where the keys are the name of the algorithm used. Define the target variable in the selected data.


```python
train_data = 'data/property_valuation/train_property_valuation.csv' ## INPUT HERE
test_data = 'data/property_valuation/test_property_valuation.csv' ## INPUT HERE
model_path = {"DT":'models/property_valuation/property_valuation_decision_tree.sav'} ## INPUT HERE
target_feature = 'price_sqm'
```

## Data and Model Ingestion

Feed the prepared input to the `load_data_model` function.


```python
X_train, y_train, X_test, y_test, train_data, test_data, model = load_data_model(train_data, test_data, model_path, target_feature)
```

## Optional Variables

The most commonly utilized variable by the tools are the list of continuous and categorical variables, and the regression flag, which determine whether the model imported is a regressor or a classifier. It is a good idea to define these variables now as the data and model are ingested.


```python
cont = X_train.select_dtypes(include = np.number).columns.tolist()
cat = X_train.select_dtypes(exclude = np.number).columns.tolist()
reg = True # regression or classification
```

## Notes
You can opt not to use the model_ingestion function, instead you can import your own data and model using `pandas` and `pickle` package, as long as the returned variables from the model ingestion function is defined. Note that the models should also be in a dictionary form, where the keys are the name of the algorithm while the values are the imported model.
