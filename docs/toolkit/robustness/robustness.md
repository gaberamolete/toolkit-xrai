---
layout: default
title: Robustness
parent: Toolkit
nav_order: 8
has_children: True
permalink: /docs/toolkit/robustness
---

# Robustness
{: .no_toc }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

## Data Preparations

Import the functions from `XRAIDashboard.robustness` and the other necessary functions.


```python
# Standard libraries
import numpy as np

# Robustness functions
from XRAIDashboard.robustness.art_mia import art_mia, art_generate_predicted, art_generate_actual, calc_precision_recall, mia_viz
from XRAIDashboard.robustness.art_metrics import pdtp_generate_samples, pdtp_metric, SHAPr_metric, visualisation
from XRAIDashboard.robustness.art_extra_models import art_extra_classifiers
```


Prepare the required data as shown below. Note that this step assumes that all the defined variables in model ingestion are also defined.


```python
pipe = model['DT'][:-1] #preprocessor pipeline
X_train_proc = pipe.transform(X_train)
X_test_proc = pipe.transform(X_test)
index_x_train = list(X_train.index)
index_x_test = list(X_test.index)


art_extra_classifiers_dict = art_extra_classifiers({'DT': model['DT']})
```

## Privacy Metric (For Classification Only)

These set of functions make use of the [Adversarial Robustness Toolbox](https://github.com/Trusted-AI/adversarial-robustness-toolbox) to evaluate the classification model in terms of privacy metric, like [Pointwise Differential Training Privacy (PDTP)](https://arxiv.org/abs/1712.09136) and [SHAPr Membership Privacy Risk](http://arxiv.org/abs/2112.02230). Follow the code snippet below to extract the score of your model to these privacy metrics.


```python
if not reg:
    pdtp_samples = 5
    shapr_samples = 5
    sample_indexes = pdtp_generate_samples(pdtp_samples, X_train_proc)
    leakage, _, _ = pdtp_metric(X_train_proc, y_train, art_extra_classifiers_dict, 'DT', threshold_value = 0, sample_indexes=sample_indexes, num_iter=1)
    text1 = f'''
            Average PDTP leakage: {np.average(leakage)} \n
            Max PDTP leakage: {np.max(leakage)}
            '''
    SHAPr_leakage, _ = SHAPr_metric(X_train_proc, y_train,
                                    X_test_proc, y_test,
                                    art_extra_classifiers_dict,
                                    'DT',threshold_value=0)
    text2 = f'''
            Average SHAPr leakage: {np.average(SHAPr_leakage)} \n
            Max SHAPr leakage: {np.max(SHAPr_leakage)}
            '''
    fig1, fig2 = visualisation(leakage, SHAPr_leakage,0,0)
```


Once the score for each metric is extracted, use the `visualisation` function to visualise the scores. Ideally, we want the scores to be less than zero, signifying that the model is robust and safe from any privacy risks.


![](../../assets/images/robustness-01.PNG)

## Membership Inference Attack (For Regression Only)

Coming from [Adversarial Robustness Toolbox](https://github.com/Trusted-AI/adversarial-robustness-toolbox) too, this tool simulates a membership inference attack where it will use a portion of the training data and the model to infer the remaining data. To utilize this, follow this code:


```python
if reg:
    train_ratio = 0.3
    inferred_train, inferred_test = art_mia(X_train_proc, y_train.to_numpy(), X_test_proc, y_test.to_numpy(), art_extra_classifiers_dict, list(model.keys())[1], attack_train_ratio=train_ratio)
    predicted = art_generate_predicted(inferred_train, inferred_test)
    actual = art_generate_actual(inferred_train, inferred_test)
    precision, recall = calc_precision_recall(predicted, actual)
    fig = mia_viz(precision,recall)
```


The resulting precision and recall shows how accurate the adversarial model in extracting the data. This will be immensely helpful in preventing the leakage of confidential data used in training the model.


![](../../assets/images/robustness-02.PNG)