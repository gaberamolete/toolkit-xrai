---
layout: default
title: Uncertainty
parent: Toolkit
nav_order: 3
has_children: True
permalink: /docs/toolkit/uncertainty
---

# Uncertainty
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

# Uncertainty
from XRAIDashboard.uncertainty.calibration import calib_lc, calib_bc, calib_temp, calib_hb, calib_ir, calib_bbq, calib_enir, calib_ece, calib_mce, calib_ace, calib_nll, calib_pl, calib_picp, calib_qce, calib_ence, calib_uce, calib_metrics, plot_reliability_diagram, my_logit, my_logistic
from XRAIDashboard.uncertainty.uct import uct_manipulate_data, uct_get_all_metrics, uct_plot_adversarial_group_calibration, uct_plot_average_calibration, uct_plot_ordered_intervals, uct_plot_XY
```

Set up the data. Our uncertainty functions need a `uct_data_dict`, which is made from the `uct_manipulate_data` function.

```python
uct_data_dict = uct_manipulate_data(X_train, X_test, y_train, y_test, model['DT'], reg = reg)
uct_data_dict
```

```text
{'y_pred': array([0., 0., 0., ..., 0., 0., 0.]),
 'y_std': 0.38740262002211606,
 'y_mean': 0.1839,
 'y_true': array([0, 0, 0, ..., 0, 0, 0]),
 'y2_mean': array([-0.1839, -0.1839, -0.1839, ..., -0.1839, -0.1839, -0.1839]),
 'y2_std': array([0.38740262, 0.38740262, 0.38740262, ..., 0.38740262, 0.38740262,
        0.38740262]),
 'X_train':            id     member_id  loan_amnt  funded_amnt  funded_amnt_inv  \
 103428   6715533   8317793     9700.0      9700.0         9700.0       
 826129  41880381  44837098    24000.0     24000.0        24000.0       
 88614    7335989   3617419    10000.0     10000.0        10000.0       
 185698   2044744   2386901    10000.0     10000.0        10000.0       
 190785   1620464   1892419     6000.0      6000.0         5975.0       
 ...          ...        ...        ...          ...              ...   
 445076  11646828  13618980    32200.0     32200.0        32200.0       
 26387     568070    730768    18000.0     18000.0        17975.0       
 117434   6166851   7648971    35000.0     35000.0        35000.0       
 171011   3153376   3866062    20000.0     20000.0        19950.0       
 66876    8666755  10438709    35000.0     35000.0        35000.0       
 
            term     int_rate  installment  grade  sub_grade  emp_length  \
 103428   36 months    11.55      320.10     1.0      7.0         5.0      
 826129   60 months    13.33      550.14     2.0     12.0        10.0      
 88614    60 months    16.20      244.25     2.0     13.0         9.0      
 185698   36 months    14.33      343.39     2.0     10.0         2.0      
 190785   36 months    13.11      202.49     1.0      8.0         0.0      
 ...            ...       ...          ...    ...        ...         ...   
 445076   60 months    21.48      879.84     4.0     21.0         2.0      
 26387    60 months    13.61      415.20     2.0     11.0         8.0      
 117434   60 months    25.80     1043.78     6.0     30.0         1.0      
 171011   60 months    17.27      499.96     2.0     14.0         1.0      
 66876    60 months    17.76      884.21     3.0     15.0         1.0      
 
        home_ownership  ...  collection_recovery_fee last_pymnt_d  \
 103428        RENT     ...            0.0             Apr-2015     
 826129        RENT     ...            0.0             Aug-2015     
 88614     MORTGAGE     ...            0.0             Sep-2014     
 185698        RENT     ...            0.0             Nov-2015     
 190785    MORTGAGE     ...            0.0             Sep-2013     
 ...               ...  ...                      ...          ...   
 445076        RENT     ...            0.0             Jun-2015     
 26387         RENT     ...            0.0             Oct-2011     
 117434    MORTGAGE     ...            0.0             Jul-2014     
 171011    MORTGAGE     ...            0.0             Sep-2015     
 66876     MORTGAGE     ...            0.0             Jul-2014     
 
        last_pymnt_amnt next_pymnt_d last_credit_pull_d  \
 103428      5047.27         NaN          Jan-2016        
 826129     23267.60         NaN          Sep-2015        
 88614       8831.62         NaN          Oct-2015        
 185698       343.00         NaN          Jan-2016        
 190785      4616.27         NaN          Jan-2016        
 ...                ...          ...                ...   
 445076      9333.74         NaN          Jan-2016        
 26387      15484.75         NaN          Oct-2011        
 117434     32107.80         NaN          Jul-2014        
 171011     12397.26         NaN          Sep-2015        
 66876      32798.31         NaN          Aug-2014        
 
        collections_12_mths_ex_med policy_code application_type  \
 103428             0.0                 1.0       INDIVIDUAL      
 826129             0.0                 1.0       INDIVIDUAL      
 88614              0.0                 1.0       INDIVIDUAL      
 185698             0.0                 1.0       INDIVIDUAL      
 190785             0.0                 1.0       INDIVIDUAL      
 ...                           ...         ...              ...   
 445076             0.0                 1.0       INDIVIDUAL      
 26387              0.0                 1.0       INDIVIDUAL      
 117434             0.0                 1.0       INDIVIDUAL      
 171011             0.0                 1.0       INDIVIDUAL      
 66876              0.0                 1.0       INDIVIDUAL      
 
         acc_now_delinq  tot_coll_amt  tot_cur_bal  total_rev_hi_lim  
 103428        0.0            0.0        50056.0         12800.0      
 826129        0.0            0.0       192328.0         59100.0      
 88614         0.0            0.0       130281.0          6700.0      
 185698        0.0            0.0        82469.0         26300.0      
 190785        0.0            0.0       169142.0         39070.0      
 ...                ...           ...          ...               ...  
 445076        0.0            0.0        52193.0         57800.0      
 26387         0.0            NaN            NaN             NaN      
 117434        0.0            0.0        44092.0         41630.0      
 171011        0.0            0.0       109768.0         41800.0      
 66876         0.0            0.0       312367.0         33600.0      
 
 [10000 rows x 50 columns],
 'X_test':            id     member_id  loan_amnt  funded_amnt  funded_amnt_inv  \
 187202   1824610   2126764    12000.0     12000.0     12000.000000     
 182447   2286309   2708571    15000.0     15000.0     15000.000000     
 199643   1496106   1756274    10000.0     10000.0     10000.000000     
 390699  16071851  18174318    16250.0     16250.0     16200.000000     
 16311     676330    864297    10000.0     10000.0      9975.000000     
 ...          ...        ...        ...          ...              ...   
 327136  23935520  26308145     4800.0      4800.0      4800.000000     
 40901     453366    560424    24250.0     24250.0     23616.169765     
 233301  37177921  39950730    29600.0     29600.0     29600.000000     
 157958   3634463   4637469    15000.0     15000.0     15000.000000     
 31762     485006    617757    11200.0     11200.0     11200.000000     
 
            term     int_rate  installment  grade  sub_grade  emp_length  \
 187202   36 months     6.03     365.23      0.0      0.0         2.0      
 182447   36 months    13.11     506.21      1.0      8.0         1.0      
 199643   36 months    14.33     343.39      2.0     10.0         1.0      
 390699   60 months    16.99     403.77      3.0     17.0         4.0      
 16311    60 months    10.00     212.48      1.0      6.0         5.0      
 ...            ...       ...          ...    ...        ...         ...   
 327136   36 months    13.35     162.55      2.0     11.0         0.0      
 40901    36 months    16.00     852.57      3.0     19.0         2.0      
 233301   36 months     6.49     907.08      0.0      1.0         6.0      
 157958   36 months    11.14     492.08      1.0      6.0         3.0      
 31762    36 months    10.25     362.71      1.0      6.0         2.0      
 
        home_ownership  ...  collection_recovery_fee last_pymnt_d  \
 187202    MORTGAGE     ...            0.0             Nov-2015     
 182447    MORTGAGE     ...            0.0             Dec-2015     
 199643        RENT     ...            0.0             Feb-2014     
 390699        RENT     ...            0.0             Jul-2015     
 16311     MORTGAGE     ...            0.0             Nov-2013     
 ...               ...  ...                      ...          ...   
 327136         OWN     ...            0.0             Nov-2015     
 40901          OWN     ...            0.0             Nov-2012     
 233301         OWN     ...            0.0             Sep-2015     
 157958    MORTGAGE     ...            0.0             Apr-2015     
 31762     MORTGAGE     ...            0.0             Sep-2010     
 
        last_pymnt_amnt next_pymnt_d last_credit_pull_d  \
 187202       365.08           NaN        Nov-2015        
 182447       505.96           NaN        Jan-2016        
 199643      6159.85           NaN        Feb-2014        
 390699       403.77           NaN        Jan-2016        
 16311        212.48           NaN        Jan-2016        
 ...                ...          ...                ...   
 327136      3199.31           NaN        Jan-2016        
 40901        911.04      Dec-2012        Feb-2015        
 233301     23653.25           NaN        Sep-2015        
 157958         3.78           NaN        Oct-2015        
 31762         10.06           NaN        Sep-2010        
 
        collections_12_mths_ex_med policy_code application_type  \
 187202             0.0                 1.0       INDIVIDUAL      
 182447             0.0                 1.0       INDIVIDUAL      
 199643             0.0                 1.0       INDIVIDUAL      
 390699             0.0                 1.0       INDIVIDUAL      
 16311              0.0                 1.0       INDIVIDUAL      
 ...                           ...         ...              ...   
 327136             0.0                 1.0       INDIVIDUAL      
 40901              0.0                 1.0       INDIVIDUAL      
 233301             0.0                 1.0       INDIVIDUAL      
 157958             0.0                 1.0       INDIVIDUAL      
 31762              0.0                 1.0       INDIVIDUAL      
 
         acc_now_delinq  tot_coll_amt  tot_cur_bal  total_rev_hi_lim  
 187202        0.0             0.0      434398.0        113300.0      
 182447        0.0             0.0       48672.0         65900.0      
 199643        0.0             0.0       50077.0         24000.0      
 390699        0.0             0.0       37608.0         23500.0      
 16311         0.0             NaN           NaN             NaN      
 ...                ...           ...          ...               ...  
 327136        0.0          1148.0       56543.0         20200.0      
 40901         0.0             NaN           NaN             NaN      
 233301        0.0             0.0      204671.0        137100.0      
 157958        0.0             0.0       88995.0         18600.0      
 31762         0.0             NaN           NaN             NaN      
 
 [2000 rows x 50 columns]}
```

## Post-hoc Calibration
Post-hoc calibration refers to the process of adjusting or refining a model or system after it has been initially developed or implemented. It involves making corrections or improvements based on observed outcomes or discrepancies between predicted and actual results. 

In machine learning or statistical modeling, post-hoc calibration is typically used to refine the outputs of a predictive model by assessing its performance on a validation dataset or by using observed outcomes that were not initially available during the model training phase.

Post-hoc calibration is particularly useful when a model's predictions are consistently overconfident or underconfident, meaning they do not accurately reflect the true probabilities or outcomes. By applying these calibration techniques, the goal is to refine the model's predictions to better match the real-world probabilities or events.

First, let's set up our predicted outputs from our model with test data as `y_pred_test`.

```python
y_pred_test = model['ElasticNet'].predict_proba(X_test)[:, 1]
```

```text
array([1.35903033e-06, 2.73052438e-03, 1.51816204e-03, ...,
       1.40556783e-02, 5.18628118e-02, 1.46596493e-07])
```

Let's look at the different post-hoc calibration techniques found in the XRAI Toolkit.

### Logistic Calibration
Also known as Platt scaling, this method trains an SVM and then trains the parameters of an additional sigmoid function to map the SVM outputs into [probabilities](https://www.researchgate.net/publication/2594015_Probabilistic_Outputs_for_Support_Vector_Machines_and_Comparisons_to_Regularized_Likelihood_Methods).

```python
lc, lc_calibrated = calib_lc(y_pred_test, y_test.to_numpy())
# 'lc' (or the first variables) gives the calibration object; the second gives the series
lc_calibrated
```

```text
array([9.61801736e-10, 1.80179206e-04, 7.04868309e-05, ...,
       2.50125729e-03, 2.09861205e-02, 2.75309920e-11])
```

### Beta Calibration
This method is a well-founded and easily implemented improvement on Platt scaling for binary classifiers. Assumes that per-class scores of classifier each follow a beta [distribution](http://proceedings.mlr.press/v54/kull17a/kull17a.pdf).

```python
bc, bc_calibrated = calib_bc(y_pred_test, y_test.to_numpy())
bc_calibrated
```

```text
array([4.93833482e-15, 3.64245479e-06, 7.53112992e-07, ...,
       2.97161903e-04, 9.89637042e-03, 1.25090120e-17])
```

### Temperature Scaling
This is a aingle-parameter variant of [Platt Scaling](https://arxiv.org/abs/1706.04599).

```python
temp, temp_calibrated = calib_temp(y_pred_test, y_test)
temp_calibrated
```

```text
array([9.18055842e-09, 3.08532088e-04, 1.37852719e-04, ...,
       2.94988133e-03, 1.83265371e-02, 4.34500738e-10])
```

### Histogram Binning
In Histogram Binning, each prediction is sorted into a bin and assigned a calibrated confidence [estimate](https://citeseerx.ist.psu.edu/viewdoc/download?doi=10.1.1.29.3039&rep=rep1&type=pdf). This is only recommended for classification use cases.

```python
hb, hb_calibrated = calib_hb(y_pred_test, y_test)
hb_calibrated
```

```text
array([0.0003058 , 0.0003058 , 0.0003058 , ..., 0.00130141, 0.00453001,
       0.0003058 ])
```

### Isotonic Regression
For classification, isotonic regression is similar to `HistogramBinning` but with dynamic bin sizes and boundaries. A piecewise constant function gets for to ground truth labels sorted by given confidence [estimates](https://www.researchgate.net/publication/2571315_Transforming_Classifier_Scores_into_Accurate_Multiclass_Probability_Estimates).

For regression, it functions as a piecewise constant, monotonically increasing mapping function used to recalibrate the estimated CDF of a probabilistic forecaster. The goal is to achieve quantile [calibration](http://proceedings.mlr.press/v80/kuleshov18a/kuleshov18a.pdf).

```python
ir, ir_calibrated = calib_ir(y_pred_test, y_test)
ir_calibrated
```

```text
array([0.00014742, 0.00045804, 0.00045804, ..., 0.00141672, 0.00277557,
       0.00014742])
```

### Bayesian Binning into Quantiles (BBQ)
This method utilizes multiple `HistogramBinning` instances with different amounts of bins, and computes a weighted sum of all methods to obtain a well-calibrated confidence [estimate](https://www.dbmi.pitt.edu/wp-content/uploads/2022/10/Obtaining-well-calibrated-probabilities-using-Bayesian-binning.pdf).

```python
bbq, bbq_calibrated = calib_bbq(y_pred_test, y_test, score = 'AIC')
bbq_calibrated
```

```text
array([0.00040218, 0.00040218, 0.00040218, ..., 0.00040235, 0.00320833,
       0.00040218])
```

### Ensemble of Near Isotonic Regression Models (ENIR)
ENIR allows a violation of monotony restrictions. Using the modified Pool-Adjacent-Violaters Algorithm (mPAVA), this method builds multiple Near Isotonic Regression Models and weights them by a certain score [function](https://ieeexplore.ieee.org/document/7837860/). This only works for classification models.

```python
enir, enir_calibrated = calib_enir(y_pred_test, y_test)
```

```text
Get path of all Near Isotonic Regression models with mPAVA ...
array([0.00014741, 0.00045758, 0.00045758, ..., 0.00140615, 0.00277182,
       0.00014741])
```

## Measuring Miscalibration
Miscalibration in a predictive model refers to the difference between predicted probabilities and the actual observed frequencies of events. It indicates how well the predicted probabilities align with the true probabilities. Analyzing miscalibration is essential to identify areas where the model's predictions might be biased or unreliable, and it guides the application of calibration techniques to improve the model's accuracy and reliability in real-world scenarios.

Let's create a variable that represents our quantiles.

```python
n_bins = 10
quantiles = np.linspace(0.1, 0.9, n_bins - 1)
quantiles
```

```text
array([0.1, 0.2, 0.3, 0.4, 0.5, 0.6, 0.7, 0.8, 0.9])
```

### Expected Calibration Error (ECE)
The ECE divides the confidence space into several bins and measures the observed accuracy in each bin. The bin gaps between observed accuracy and bin confidence are summed up and weighted by the amount of samples in each [bin](https://www.dbmi.pitt.edu/wp-content/uploads/2022/10/Obtaining-well-calibrated-probabilities-using-Bayesian-binning.pdf).

```python
cece = calib_ece(y_pred_test, y_test, 100)
cece
```

```text
0.014646379825497742
```

### Maximum Calibration Error (MCE)
The MCE denotes the highest gap over all [bins](https://www.dbmi.pitt.edu/wp-content/uploads/2022/10/Obtaining-well-calibrated-probabilities-using-Bayesian-binning.pdf).

```python
cmce = calib_mce(y_pred_test, y_test, 100)
cmce
```

```text
0.626835218343391
```

### Average Calibration Error (ACE)
This denotes the average miscalibration where each bin gets weighted [equally](https://openreview.net/pdf?id=S1lG7aTnqQ).

```python
cace = calib_ace(y_pred_test, y_test, 100)
cace
```

```text
0.23693357334526946
```

### Negative Log Likelihood (NLL)
This method measures the quality of a predicted probability distribution with respect to the ground truth.

```python
nll = calib_nll(y_pred_test_means, y_pred_test_stds, y_test)
nll
```

```text
117.78346541312209
```

### Pinball Loss
A synonym for Quantile Loss, this method is a quantile-based calibration. This tests for quantile calibration of a probabilistic regression model. This is an asymmetric loss that measures the quality of the predicted quantiles.

```python
pl = calib_pl(y_pred_test_means, y_pred_test_stds, y_test)
pl
```

```text
0.04408728063359086
```

### Prediction Interval Coverage Probability (PICP)
The is a quantile-based calibration used for Bayesian models to determine quality of the uncertainty estimates. In Bayesian mode, an uncertainty estimate is attached to each sample. The PICP measures the probability that the true (observed) accuracy falls into the $p\%$ prediction [interval](https://arxiv.org/pdf/1906.09686.pdf). Our function returns the Prediction Interval Coverage Probability (PICP) and the Mean Prediction Interval Width (MPIW).

```python
picp, mpiw = calib_picp(y_pred_test_means, y_pred_test_stds, y_test)
picp, mpiw
```

```text
(0.6404530240523079, 0.5965177759204162)
```

### Quantile Calibration Error (QCE)
This is another quantile-based calibration that returns the Marginal Quantile Calibration Error (M-QCE), which measures the gap between predicted quantiles and observed quantile coverage for multivariate distributions. This is based on the Normalized Estimation Error Squared (NEES), known from [object tracking](https://arxiv.org/pdf/2207.01242.pdf).

```python
qce = calib_qce(y_pred_test_means, y_pred_test_stds, y_test)
qce
```

```text
0.26493431237729514
```

### Expected Normalized Calibration Error (ENCE)
This is a variance-based calibration used for normal distributions, where we measure the quality of the predicted variance/stddev estimates. We require that the predicted variance matches the observed error variance, which is equivalent to the Mean Squared Error. ENCE applies a binning scheme with $B$ bins over the predicted standard deviation $ \sigma_y (X) $ and measures the absolute (normalized) difference between RMSE and [RMV](https://arxiv.org/pdf/1905.11659.pdf).

```python
ence = calib_ence(y_pred_test_means, y_pred_test_stds, y_test)
ence
```

```text
3.108876468414131
```

### Uncertainty Calibration Error (UCE)
UCE is similar to ENCE, but applies a binning scheme with B bins over the predicted variance $\sigma^{2}_{y} (X)$ and measures the absolute difference between MSE and [MV](http://proceedings.mlr.press/v121/laves20a/laves20a.pdf).

```python
uce = calib_uce(y_pred_test_means, y_pred_test_stds, y_test)
uce
```

```text
0.1387100096725775
```

### Other Standard Metrics
We summarize some standard performance and calibration metrics through `uct_get_all_metrics`.
- Adversarial Group Calibration: An extension of Expected Calibration Error (ECE), as it requires average calibration of any subset of X with any non-zero measure. We can measure this by measuring the average calibration within all subsets of data with sufficiently many points.
- Sharpness: Sharpness quantifies the tightness, concentration, or peakedness of the predictive distribution. It solely assesses the predictive distribution without factoring in the individual data point or the actual distribution of ground truth when determining its measure. 
- Continuous Ranked Probability Score (CRPS): a negatively oriented (smaller value is desirable) general score for continuous distribution predictions, usually for Gaussian distributions.
- Check Score: Also known as pinball loss
- Interval Score: A negatively oriented proper scoring rule for centered prediction intervals, computed by scanning over a sequence of prediction intervals.

```python
uct_metrics = uct_get_all_metrics(uct_data_dict)
uct_metrics
```

```text
(1/n) Calculating accuracy metrics
(2/n) Calculating average calibration metrics
(3/n) Calculating adversarial group calibration metrics
[1/2] for mean absolute calibration error
Measuring adversarial group calibration by spanning group size between 0.0 and 1.0, in 10 intervals
100%|███████████████████████████████████████████| 10/10 [00:02<00:00,  3.76it/s]
[2/2] for root mean squared calibration error
Measuring adversarial group calibration by spanning group size between 0.0 and 1.0, in 10 intervals
100%|███████████████████████████████████████████| 10/10 [00:02<00:00,  3.78it/s]
(4/n) Calculating sharpness metrics
(n/n) Calculating proper scoring rule metrics
**Finished Calculating All Metrics**


===================== Accuracy Metrics =====================
MAE           0.184
RMSE          0.184
MDAE          0.184
MARPD         166.944
R2            0.775
Correlation   1.000
=============== Average Calibration Metrics ================
Root-mean-squared Calibration Error   0.299
Mean-absolute Calibration Error       0.241
Miscalibration Area                   0.242
========== Adversarial Group Calibration Metrics ===========
Mean-absolute Adversarial Group Calibration Error
    Group Size: 0.11 -- Calibration Error: 0.243
    Group Size: 0.56 -- Calibration Error: 0.241
    Group Size: 1.00 -- Calibration Error: 0.241
Root-mean-squared Adversarial Group Calibration Error
    Group Size: 0.11 -- Calibration Error: 0.300
    Group Size: 0.56 -- Calibration Error: 0.299
    Group Size: 1.00 -- Calibration Error: 0.299
==================== Sharpness Metrics =====================
Sharpness   0.438
=================== Scoring Rule Metrics ===================
Negative-log-likelihood   0.155
CRPS                      0.132
Check Score               0.067
Interval Score            0.749
```

## Visualizing Uncertainty
Comparing calibration metrics involves evaluating multiple metrics used to assess the calibration performance of predictive models. These metrics provide different perspectives on how well a model's predicted probabilities align with the actual outcomes.

Choose calibration metrics that suit the needs of your analysis. For example, if you are interested in overall calibration performance, then metrics such as the Expected Calibration Error (ECE) will be more suitable. If you want to pinpoint critical areas needing calibration improvement, use Maximum Calibration Error (MCE). Recognize that different metrics may emphasize different aspects of calibration. Some metrics might prioritize accuracy over the entire probability range, while others might focus on specific regions or overall trends. 

Remember when comparing calibration metrics between different models, algorithms, or variations of the same model, to ensure a consistent evaluation across all models using the same evaluation dataset.

### Calibration Metrics Table
We provide a function `calib_metrics` that summarizes the calibration metrics of different calibration techniques.

```python
calibs = {
    'Uncalibrated': y_pred_test,
    'Logistic Calibration': lc_calibrated,
    'Beta Calibration': bc_calibrated,
    'Temperature Scaling': temp_calibrated,
    'Histogram Binning': hb_calibrated,
    'Isotonic Regression': ir_calibrated,
    'Bayesian Binning into Quantiles': bbq_calibrated,
    'Ensemble of Near Isotonic Regression': enir_calibrated
}
calibs_df = calib_metrics(y_test, calibs, n_bins)
calibs_df
```

![](../../assets/images/uncertainty_01-calib_table.PNG)

### Reliability Diagram
A reliability diagram is a graphical tool used to visually assess the calibration performance of a predictive model. It helps in evaluating how well a model's predicted probabilities align with the actual observed frequencies or outcomes.

Interpretation of a reliability diagram involves examining the pattern of points relative to the diagonal line. Ideally, the points should cluster around the diagonal, indicating good calibration. Dispersed or systematically shifted points away from the diagonal suggest areas where the model's predicted probabilities are miscalibrated. If the points lie below the diagonal line, it suggests that the model is overconfident (predicting higher probabilities than the observed frequencies). Points above the diagonal line indicate the model is underconfident (predicting lower probabilities than the observed frequencies).

```python
calibs = {
    'Logistic Calibration': [lc_calibrated, lc],
    'Beta Calibration': [bc_calibrated, bc],
    'Temperature Scaling': [temp_calibrated, bc],
    'Histogram Binning': [hb_calibrated, hb],
    'Isotonic Regression': [ir_calibrated, ir],
    'Bayesian Binning into Quantiles': [bbq_calibrated, bbq],
    'Ensemble of Near Isotonic Regression': [enir_calibrated, enir]
}
for k, v in calibs.items():
    fig = plot_reliability_diagram(y_test, v[0], v[1], title = k, error_bars = True, n_bins = 50)
```

![](../../assets/images/uncertainty_02-rd_logistic.PNG)

![](../../assets/images/uncertainty_03-rd_beta.PNG)

![](../../assets/images/uncertainty_04-rd_temp.PNG)

![](../../assets/images/uncertainty_05-rd_hb.PNG)

![](../../assets/images/uncertainty_06-rd_ir.PNG)

![](../../assets/images/uncertainty_07-rd_bbq.PNG)

![](../../assets/images/uncertainty_08-rd_enir.PNG)


These plots visualize over- and underconfidence with the re-calibrated scores, while also displaying an estimaetd Miscalibrated Area. Candlesticks at positions around the diagonal also express likely locations of outcomes under the mentioned probability.

### Adversarial Group Calibration
A metric that was introduced by [Zhao et. al.](https://arxiv.org/abs/2006.10288), this involves taking many random subsets of the test data, computing miscalibration on each subset, and then reporting the worst miscalibration across the subsets. The plot below shows this metric as we vary the size of the subsets constructed ($x$-axis). For each subset size the procedure is repeated several times and the shaded region shows the standard error. Note that an individually calibrated model should have low calibration error for any group size.

We plot adversarial group calibration by varying subsets of varying size, from 0 to 100% of the dataset size, and recording the worst calibration occurring for each group size.

```python
agc = uct_plot_adversarial_group_calibration(uct_metrics)
agc
```

![](../../assets/images/uncertainty_09-agc.PNG)