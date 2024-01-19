---
layout: default
title: XRAIDashboard.model_ingestion.data_model
parent: Model Ingestion
grand_parent: Toolkit
nav_order: 1
---

# XRAIDashboard.model_ingestion.data_model.load_data_model
**[XRAIDashboard.model_ingestion.data_model.load_data_model(train_data, test_data, model_path, target_feature)](https://github.com/gaberamolete/XRAIDashboard/blob/main/model_ingestion/data_model.py)**


Automate the ingestion process of data and model given a file location for the train data, test data, and model.


**Parameters:**
- train_data (str): File location of the csv file of the train data
- test_data (str): File location of the csv file of the test data
- model (dict): A dictionary containing all the model path for ingestion with key as the name of the model
- target feature (str): Target variable of the data and model

**Returns:**
- train_x (pandas.DataFrame): X_train
- train_y (pandas.DataFrame): y_train
- test_x (pandas.DataFrame): X_test
- test_y (pandas.DataFrame): y_test
- train_data (pandas.DataFrame): Train data
- test_data (pandas.DataFrame): Test data
- models (dict): Dictionary containing all the models

