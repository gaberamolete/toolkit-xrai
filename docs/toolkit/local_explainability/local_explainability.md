---
layout: default
title: Local Explainability
parent: Toolkit
nav_order: 5
has_children: True
permalink: /docs/toolkit/local_explainability
---

# Local Explainability
{: .no_toc }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

## Data Preparations

Import packages and data.

```python
# Call functions
import warnings
warnings.filterwarnings("ignore")

import pandas as pd
import numpy as np
import shap
shap.initjs()

# Display
from IPython.display import display
from sklearn.pipeline import Pipeline
from sklearn import set_config
set_config(display = 'diagram')


# Global explanation
from XRAIDashboard.local_exp.local_exp import dice_exp, exp_cf, Predictor, get_feature_names, exp_qii, dalex_exp, break_down, interactive, cp_profile, initiate_shap_loc, shap_waterfall, shap_force_loc, shap_bar_loc
```

Set up the data. Since we're looking at local explanations, we need to identify a single index.

```python
idx = 5 # Placeholder
```

Set up the SHAP-based functionalities.

```python
class_names = ['Accepted', 'Rejected']
loc_exp, shap_value_loc, feature_names = initiate_shap_loc(X_train[:2000], model['DT'][-1], preprocessor, cat_cols)
shap_value_loc
```

```text
.values =
array([[ 2.77483789e+01, -8.17397575e+04,  5.57640190e-01, ...,
         1.05159104e+04,  1.43060607e+03, -9.43190834e+01],
       [ 0.00000000e+00, -1.05202633e+05,  0.00000000e+00, ...,
         5.98299611e+03, -2.11116736e+02, -1.70139884e+02],
       [ 6.31303937e+01, -2.91048360e+05,  0.00000000e+00, ...,
         3.59858620e+03,  4.16017590e+01, -5.59024738e+01],
       ...,
       [ 0.00000000e+00, -7.17673806e+04,  0.00000000e+00, ...,
         1.49460982e+04, -3.46926118e+02,  4.29893799e-01],
       [ 6.98928250e+01, -1.23719030e+05,  0.00000000e+00, ...,
         5.20309871e+03, -8.45395172e+02, -7.97472144e+02],
       [ 0.00000000e+00, -7.30734128e+04,  0.00000000e+00, ...,
        -4.80079437e+03, -7.78955143e+02, -7.57565345e+02]])

.base_values =
array([389790.12117366, 389790.12117366, 389790.12117366, ...,
       389790.12117366, 389790.12117366, 389790.12117366])

.data =
array([[ 0.        ,  0.        ,  0.        , ..., -0.50954921,
         0.74851399, -0.51671495],
       [ 0.        ,  0.        ,  0.        , ..., -0.24486812,
        -0.755073  , -0.71383756],
       [ 0.        ,  0.        ,  0.        , ..., -0.24486812,
        -0.755073  , -0.71383756],
       ...,
       [ 0.        ,  0.        ,  0.        , ..., -0.77423031,
        -0.755073  ,  0.50387143],
       [ 0.        ,  0.        ,  0.        , ...,  0.81385627,
        -0.0032795 ,  0.81227293],
       [ 0.        ,  0.        ,  0.        , ...,  1.87258066,
        -0.0032795 ,  0.84724629]])
```

## DiCE
Diverse Counterfactual Explanations (DiCE) is a tool developed by Microsoft that provides counterfactual explanations for machine learning models. Counterfactual explanations are a type of explanation that can help users understand why a machine learning model made a particular prediction or decision. They do this by showing what changes would need to be made to the input features of a model in order to change its output.

DiCE is designed to address a common problem with counterfactual explanations: they can often provide only a single, arbitrary solution for how to change the input features. This can be limiting, as it may not give the user a full understanding of how the model is working, or how changes to the input features would impact the output.

To overcome this limitation, DiCE generates multiple counterfactual explanations that are diverse and meaningful. Specifically, DiCE generates a set of counterfactual explanations that satisfy two criteria:
- Relevance: Each counterfactual explanation should be as close as possible to the original input while still changing the model's output. In other words, the changes made to the input should be minimal, to avoid making changes that would not be realistic or practical.
- Diversity: Each counterfactual explanation should be different from the others in the set, in order to provide a range of possible explanations for the model's output.

DiCE uses an optimization algorithm to generate these counterfactual explanations. The algorithm searches for the smallest possible change to the input features that would change the model's output, subject to the constraint that each counterfactual explanation should be diverse from the others in the set.

```python
exp1 = dice_exp(X_train, y_train, model['DT'], target = target[0])
e2 = exp_cf(X = X, exp = exp1, total_CFs = 2, features_to_vary = ['int_rate', 'total_pymnt'])
```

A sample output is found below:

![](../../assets/images/local_exp_01-dice.PNG)

In here, we are looking at a dataframe determining the income class of certain applicants for a loan. The original instance has an outcome of "0", and we are looking to find the combinations of factors to change the appplicant's outcome to 1. The algorithm finds that either a change in `workclass`, `education`, or `occupation` is needed.

Users can also specify if they want only certain columns to be changed, or if there is a permitted range of items for each column.

## Quantitative Input Influence
Quantitative Input Influence (QII) is a method for quantifying the impact of each input feature on the model's output. QII can be used to identify which input features are most important to the model's decision, and how changes to those features would impact the output.

QII works by computing the partial derivatives of the model's output with respect to each input feature. These derivatives indicate how sensitive the model's output is to changes in each feature. By computing the absolute values of these derivatives, QII can rank the input features in order of importance, from most to least influential.

Once the input features have been ranked, QII can be used to generate counterfactual explanations that show how changes to specific input features would impact the model's output. These counterfactual explanations can be used to understand the logic behind the model's decision, and to identify potential biases or errors in the model.

For example, if a model is being used to predict loan approvals, QII could be used to identify which input features are most important to the model's decision, such as income, credit score, and employment history. By generating counterfactual explanations that show how changes to these features would impact the model's output, users can better understand how the model is making its decisions, and identify potential biases or errors in the model. 

More info in https://www.andrew.cmu.edu/user/danupam/datta-sen-zick-oakland16.pdf

```python
# For classification
qii_vals, fig = exp_qii(model['DT'][-1], X_test, idx, preprocessor)
qii_vals
```

![](../../assets/images/local_exp_02-qii1.PNG)

![](../../assets/images/local_exp_03-qii2.PNG)

## Break Down Plots
How can your model response be explained by the model's features? What are the most important features of the model? This function is best for why questions, or when you have a moderate number of features. Just be careful when features are correlated.

Break-down plots show how the contributions attributed to the individual explanatory variables can change the average model's prediction in order to yield the actual prediction for a single observation (hence local explanation).

The first row (`intercept`) showcases the mean value of the model's predictions for all data. The subsequent rows show the distribution and mean values of the predictions when we fix values to certain explanatory variables. The last row (`prediction`) showcases the prediction for the observation of interest. The green and red bars should indicate positive and negative changes in the mean predictions.

Ideally, you would want the end of your last rows to be in line nearer the prediction. This would mean that the fixed order of the explanatory variables are enough to give a good explanation of what is happening with your particular observation of interest.

```python
exp, obs = dalex_exp(model["DT"], X_train, y_train, X_test, idx)
break_down(exp, obs)
```

![](../../assets/images/local_exp_04-bd1.PNG)

A break-down graph such as the one below may leave a wanting explanation to what is happening with a particular observation of interest.

![](../../assets/images/local_exp_05-bd2.PNG)

![](../../assets/images/local_exp_06-bd3.PNG)

The table that comes with the output is a tabular explanation of the graph. Each row is an explanatory variable found in the data/model, sorted descending contribution (`contribution` in the table) to the explanation. Each `variable_name` is paired with the `variable_value` of the specific point of observation, while `variable` is the concatenation of these two columns. The `cumulative` variable showcases the value starting from the `intercept`, now modified due to the `contribution` of each variable/row. The `sign` column denotes whether the `contribution` is positive or negative.

### Additive Break Down
How does the average model response change when new features are being fixed in the observation of interest? What if we force a specific order of variables?

```python
order = ['grade', 'loan_amnt', 'dti', 'home_ownership', 'purpose']
break_down(exp, obs, order)
```

![](../../assets/images/local_exp_07-abd_graph.PNG)

![](../../assets/images/local_exp_08-abd_table.PNG)

### Interactive Break Down
The effects of an explanatory variable depends on the values of other variables. How does that affect the model response? We focus on pairwise interactions.

This may take a while depending on the model and number of variables you have.

```python
interactive(exp, obs, count = 10)
```

![](../../assets/images/local_exp_09-ibd_graph.PNG)

![](../../assets/images/local_exp_10-ibd_table.PNG)

Interaction with respect to model explanations posits that the effect or contribution of a single explanatory variable depends on the values of other explanatory variables. To showcase, below is an example of a probability table with the famous *Titanic* dataset, considering two variables: *age* and *class*. Let's look at a simplified version where *age* only has two levels: kids (0-16 years old) and adults (17+ years old). For *class*, let's just consider "2nd class" and "Other".

| Class | Kids (0-16) | Adults (17+) | Total |
| --- | --- | --- | --- |
| 2nd | 11/12 = 91.7%  | 13/166 = 7.8% | 24/178 = 13.5% |
| Other | 2269 = 31.9% | 306/1469 = 20.8% | 328/1538 = 21.3% |
| Total | 33/81 = 40.7% | 319/1635 = 19.5% | 352/1716 = 20.5% |

The overall probability of survival for people in the Titanic is 20.5%, but for passengers from the 2nd class, it is even lower at 13.5%. We can say that the effect of being 2nd class is negative, as it decreased the survival probability by 7%. However, if we look at kids in the 2nd class only, the probability increases by 78.2% to 91.7%. Thus by looking first at *class* then *age*, we can get -7% for *class* and +78.2% for *age*.

However, if you first consider *age*, you could see that the probability for being a kid is higher at 40.7%, increasing by 20.2%. Then for kids, travelling in the 2nd class further increases the probability to 91.7%, increasing by 51%. We can then say that by looking first at *age* then *class*, we can get +20.2% for *age* and +51% for *class*.

Thus, by considering the effects in a different order, we get different contributions attributed to the variables. Looking at the table, we can conclude that the overall effect of the 2nd class in *class* is negative by -7% (decreasing from 20.5% to 13.5%), and that being a kid in *age* has a positive effect of +20.2% (increasing from 20.5% to 40.7%). We can expect a probability of 20.5% - 7% + 20.2% = 33.7% for a kid in 2nd class, but the observed proportion of survivors in that category is higher (91.7%). Thus, we can say that the interaction effect is 91.7% - 33.7% = 58%, an additional effect of the 2nd class specific for kids.

We take advantage of this kind of analysis to showcase these interactions in break-down plots. Below, we can see that the break-down plot does a subpar job of sufficiently explaining the model effect on this particular observation, as all other factors need to account for a 0.29 difference to match the actual prediction.

![](../../assets/images/local_exp_11-ibd_graphbad.PNG)

However, if we introduce interactions to the plot, we may see that certain interactions between variables, when looked at together, seem to have a better explanation of the model effect compared to the initial break-down plot.

![](../../assets/images/local_exp_12-ibd_graphgood.PNG)

Please note that utilizing interactions is not based on any formal statistical-significance test. Thus, this may lead to false-positive findings especially in small sample sizes.

## Ceteris Paribus
How would the model response change for a particular observation if only a single feature is changed? This function is best for what if questions. Just be careful when features are correlated.

```python
# Numerical variables
cp_profile(exp, obs, variables = ['grade', 'loan_amnt', 'dti'])
```

![](../../assets/images/local_exp_13-cp_numerical.PNG)

```python
# Categorical variables
cp_profile(exp, obs, variables = ['home_ownership', 'purpose'], var_type = 'categorical')
```

![](../../assets/images/local_exp_14-cp_categorical.PNG)

## Waterfall Plot
The waterfall plot explanation shows features each contributing to push the model output from the base value (the average model output over the training dataset we passed) to the model output. Features pushing the prediction higher are shown in red, those pushing the prediction lower are in blue.

```python
shap_waterfall(shap_value_loc, idx, feature_names = feature_names, class_ind = 1, class_names = class_names)
```

![](../../assets/images/local_exp_15-waterfall1.PNG)

The example above attempts to explain the likelihood of default of a loan applicant. The `f(x)` showcases the probability of the observation to be the "1" class, or in the model's terms, the likelihood to default or have a "Rejected" application. The model's mean predictions are showcased with `E[f(x)]`, a line shooting up from the bottom of the graph. As shown, while the model mostly predicts in the "0" class, or "Accepted" applications, this particular observation has a high probability of rejection, at 0.972. We can see that the main contributors of this likely rejection are the variables `num__total_rec_prncp`, `num__total_pymnt`, and `num__last_pymnt_amnt`, with +0.29, +0.17, and +0.13 respectively.

For classification models, we can also specify the likelihood of getting other classes.

```python
shap_waterfall(shap_value_loc, idx, feature_names = feature_names, class_ind = 0, class_names = class_names)
```

![](../../assets/images/local_exp_16-waterfall2.PNG)

Using the same example as above, we can see that the `f(x)` now pertains to the likelihood to get a "0" class, or an "Accepted" application. Thus, the same observation is highly unlikely to get this class, with a 0.028 or a 1 - 0.972 probability. We can see now that the effects of each explanatory variable are now inversed, with `num__total_rec_prncp` having significant negative (or blue) effects. The `E[f(x)]` value has also flipped due to the binary nature of the model.

## Force Plot
The local force plot attempts to summarize all the individual rows found in a waterfall plot in one continuous, additive "force". As with the previous plot, features pushing the prediction higher are shown in red, those pushing the prediction lower are in blue. 

```python
shap_force_loc(shap_value_loc, idx, feature_names, 1, class_names)
```

![](../../assets/images/local_exp_17-force1.PNG)

Take for example the plot above, a force plot equivalent of the waterfall plot example shown previously. We know that the `f(x)` of this observation is around 0.97, as shown in bold on the right. We know that the `E[f(x)]`, now written as a `base value` is around 0.23. The force plot conveys that `total_rec_prncp` =-1.2265.. and `total_pymnt` = -1.2487.. contribute the most to that higher probability for this observation. 

Similarly to the waterfall plot, we can explain plots for other classes in classification models.

```python
shap_force_loc(shap_value_loc, idx, feature_names, 0, class_names)
```

![](../../assets/images/local_exp_18-force2.PNG)

As with before, the `f(x)`, showcasing the likelihood for the observation to be in the "Accepted" class, is now at 0.03; the `base value` also changed accordingly. We still see the main variables `num__total_rec_prncp`, `num__total_pymnt`, and `num__last_pymnt_amnt`, just flipped (as with the color blue).

## Bar Plot
This is another interpretation of the waterfall and local force plots, brought to you in a double-sided feature importance plot.

![](../../assets/images/local_exp_19-bar1.PNG)

Compared to the first two plots, this does not give an `f(x)` nor `E[f(x)]` indicator. The picture above showcases the same observation, noting that the variables significantly contribute to a higher likelihood of the "Rejected" class. While it does not show the actual values of each variable for that observation, the local bar plot does further emphasize the individual SHAP value contributions.

![](../../assets/images/local_exp_20-bar2.PNG)