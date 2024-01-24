---
layout: default
title: Dashboard
parent: Toolkit
nav_order: 9
---

# Dashboard
{: .no_toc }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

## Data Preparations
Firstly, import the dashboard functions and other required libraries.

```python
# Standard Libraries
%matplotlib inline
import pandas as pd
import numpy as np
import joblib
from sklearn.pipeline import Pipeline

import warnings
warnings.filterwarnings("ignore")

from explainerdashboard import *
import dash_bootstrap_components as dbc

from raiwidgets.responsibleai_dashboard import ResponsibleAIDashboard
from raiwidgets import ErrorAnalysisDashboard

# Display
from IPython.display import display
from sklearn.pipeline import Pipeline
from sklearn import set_config
set_config(display = 'diagram')

import shap
shap.initjs()

#ExplainerDashboard
from XRAIDashboard.eda.dashboard import BlankComponent, AutoVizComponent, EDATab
from XRAIDashboard.fairness.dashboard import BlankComponent, FairnessIntroComponent, FairnessCheckRegComponent, FairnessCheckClfComponent, ModelPerformanceRegComponent, ModelPerformanceClfComponent, OutlierComponent, ErrorAnalysisComponent, FairnessTab
from XRAIDashboard.local_exp.dashboard import BlankComponent, EntryIndexComponent, BreakDownComponent, AdditiveComponent, CeterisParibusComponent, InteractiveComponent, DiceExpComponent, QIIExpComponent, ShapWaterfallComponent, ShapForceComponent, ShapBarComponent, LocalExpTab
from XRAIDashboard.global_exp.dashboard import BlankComponent, PartialDependenceProfileComponent, VariableImportanceComponent, LocalDependenceComponent, AccumulatedLocalComponent, CompareProfileComponent, ShapBarGlobalComponent, ShapSummaryComponent, ShapDependenceComponent, ShapForceGlobalComponent, GlobalExpTab
from XRAIDashboard.stability.dashboard import BlankComponent, PSIComponent, KSTestComponent, DataDriftComponent, DataDriftTestComponent, DataQualityComponent, DataQualityTestComponent, TargetDriftComponent, RegressionPerformanceComponent, RegressionPerformanceTestComponent, ClassificationPerformanceComponent, ClassificationPerformanceTestComponent, AlibiCVMComponent, AlibiFETComponent, DecileComponent, StabilityTab
from XRAIDashboard.robustness.dashboard import BlankComponent, ARTPrivacyComponent, ARTInferenceAttackComponent, RobustnessTab
from XRAIDashboard.uncertainty.dashboard import BlankComponent, CalibrationComponent, AdversarialCalibrationComponent, AverageCalibrationComponent, OrderedIntervalsComponent, XYComponent, UncertaintyTab
```


Same from the model ingestion, import the data and model using the `load_data_model` function.

```python
train_data = 'data/property_valuation/train_property_valuation.csv' ## INPUT HERE
test_data = 'data/property_valuation/test_property_valuation.csv' ## INPUT HERE
model_path = {"LGBM":'models/property_valuation/property_valuation_lgbm.sav',"DT":'models/property_valuation/property_valuation_decision_tree.sav'} ## INPUT HERE
target_feature = 'price_sqm' ## INPUT HERE

X_train, y_train, X_test, y_test, train_data, test_data, model = load_data_model(train_data, test_data, model_path, target_feature)

cont = X_train.select_dtypes(include = np.number).columns.tolist()
cat = X_train.select_dtypes(exclude = np.number).columns.tolist()
reg = True
```


Then, prepare the required data for all the functions you want to include in the dashboard.


```python
# Configure your sklearn pipeline here
pipe = Pipeline(
    steps = [
        ('step1', model['DT'][0]),
        ('step2', model['DT'][1])
    ]
)

pipe.fit(X_train, y_train)
```

```python
# Configure your sklearn pipeline here
pipe = Pipeline(
    steps = [
        ('step1', model['DT'][0]),
        ('step2', model['DT'][1])
    ]
)

pipe.fit(X_train, y_train)
```


```python
# Configure the groupings for the Grouped Variable Importances Component in the Dashboard. Set to None for no groupings
if reg:
    variable_groups = {
        'cmci': ['infrastructure', 'resiliency', 'productivity', 'security', 'transparency', 'utilities'],
        'house_amenities': [ 'ac_unit', 'balcony', 'deck', 'fence', 'fireplace', 'fitness_center', 'garage',
                            'grass', 'library_books', 'local_airport', 'local_parking', 'meeting_room', 'park',
                            'pool', 'security.1', 'smoke_free', 'sports_basketball', 'sports_tennis',
                            'sports_volleyball', 'warehouse', 'yard'],
        'house_characteristics': ['price_conditions', 'car_spaces', 'bedrooms', 'bathrooms', 'floor_area', 'land_size'],
        'LOI_1000': ['cafe_1000', 'fast_food_1000', 'pub_1000', 'restaurant_1000', 'college_1000', 'kindergarten_1000',
                    'school_1000', 'university_1000', 'fuel_1000', 'parking_1000', 'atm_1000', 'bank_1000', 'clinic_1000',
                    'hospital_1000', 'pharmacy_1000', 'police_1000', 'townhall_1000', 'marketplace_1000', 'hotel_1000',
                    'residential_1000', 'commercial_1000', 'industrial_1000', 'retail_1000', 'supermarket_1000',
                    'fire_station_1000', 'government_1000'],
        'LOI_3000': ['cafe_3000', 'fast_food_3000', 'pub_3000', 'restaurant_3000', 'college_3000', 'kindergarten_3000',
                    'school_3000', 'university_3000', 'fuel_3000', 'parking_3000', 'atm_3000', 'bank_3000', 'clinic_3000',
                    'hospital_3000', 'pharmacy_3000', 'police_3000', 'townhall_3000', 'marketplace_3000', 'hotel_3000',
                    'residential_3000', 'commercial_3000', 'industrial_3000', 'retail_3000', 'supermarket_3000',
                    'fire_station_3000', 'government_3000'],
        'LOI_5000': ['cafe_5000', 'fast_food_5000', 'pub_5000', 'restaurant_5000', 'college_5000', 'kindergarten_5000',
                    'school_5000', 'university_5000', 'fuel_5000', 'parking_5000', 'atm_5000', 'bank_5000', 'clinic_5000',
                    'hospital_5000', 'pharmacy_5000', 'police_5000', 'townhall_5000', 'marketplace_5000', 'hotel_5000',
                    'residential_5000', 'commercial_5000', 'industrial_5000', 'retail_5000', 'supermarket_5000',
                    'fire_station_5000', 'government_5000'],
        'socio-economic': ['LGU', 'poverty_inc', 'subs_inc', 'lgu_type', 'income_class', 'anreg_income_2021',
                        'capex_2021', 'socex_2021', 'pop_2022', 'growth_5years', 'growth_10years']
    }
elif not reg:
    variable_groups = {
        'total': ['total_acc', 'total_pymnt', 'total_pymnt_inv', 'total_rec_prncp',
                    'total_rec_int', 'total_rec_late_fee', 'total_rev_hi_lim'],
            'amount': ['loan_amnt', 'funded_amnt', 'funded_amnt_inv', 'last_pymnt_amnt'],
            'categorical': X_train.select_dtypes(exclude = ['int64', 'float64']).columns.tolist()
    }
```


```python
# Separate continuous and categorical variables
cont = X_train.select_dtypes(include = ['int64', 'float64']).columns.tolist()
cat = X_train.select_dtypes(exclude = ['int64', 'float64']).columns.tolist()
```


```python
# Only one model should be selected, and it should be in a dictionary form
model_selected = {'DT': model['DT']}
if reg:
    model_type = 'regressor'
elif not reg:
    model_type = 'classifier'
is_sklearn_pipe = True # Did it use sklearn pipeline?
```


```python
# Create a Dalex explainer for the global explanation components
exp, obs = dalex_exp(list(model_selected.values())[0], X_train, y_train, X_test, 0)
```


```python
dataset = pd.concat([train_data, test_data], axis=0)
dataset.info()
```


```python
if reg:
    try:
        features = pipe.get_feature_names_out()
    except:
        try:
            features = pipe.get_feature_names_out()
            print('Preprocessing - Normal')
        except:
            try:
                p_ind = pipe[-1].get_support(indices = True)
                fn = pipe[0].get_feature_names_out()
                features = [fn[x] for x in p_ind]
                print('Preprocessing - Steps')
            except:
                try:
                    features = get_feature_names(pipe, cat)
                    print('Preprocessing (old) - Normal')
                except:
                    p_ind = pipe[-1].get_support(indices = True)
                    fn = get_feature_names(pipe[0], cat)
                    features = [fn[x] for x in p_ind]
                    print('Preprocessing (old) - Steps')
    pipe.fit(X_train)
    X_train_proc = pd.DataFrame(pipe.transform(X_train), columns=features)
    X_test_proc = pd.DataFrame(pipe.transform(X_test), columns=features)
elif not reg:
    try:
        features = pipe.get_feature_names_out()
    except:
        features = get_feature_names(preprocessor, cat_cols)
        p_ind = preprocessor[-1].get_support(indices = True)
        fn = get_feature_names(preprocessor[0], cat_cols)
        features = [fn[x] for x in p_ind]
    preprocessor.fit(X_train)
    X_train_proc = pd.DataFrame(preprocessor.transform(X_train), columns=features)
    X_test_proc = pd.DataFrame(preprocessor.transform(X_test), columns=features)
train_data_proc = pd.concat([X_train_proc, y_train], axis=1) if model_type == "classifier" else None
test_data_proc = pd.concat([X_test_proc, y_test], axis=1) if model_type == "classifier" else None
```

Run the dashboard and functions that generates HTML reports so the dashboard can readily import them.

```python
ydata_profiling_eda2(dataset.sample(10))
autoviz_eda2(dataset.sample(100))

if model_type == 'classifier':
    target_feature = target[0]
    drop_cols = ['id', 'member_id', 'issue_d', 'title', 'zip_code', 'addr_state', 'last_pymnt_d',
             'next_pymnt_d', 'last_credit_pull_d', 'tot_coll_amt', 'tot_cur_bal', 'total_rev_hi_lim']
    num_cols = list(set(dataset.select_dtypes(include = ['int64', 'float64']).columns.tolist()) - set(drop_cols) - set(target_feature))
    cat_cols = list(set(dataset.select_dtypes(exclude = ['int64', 'float64']).columns.tolist()) - set(drop_cols) - set(target_feature))
    rai_insights, cohort_list = xrai_features(list(model_selected.values())[0], train_data.drop(drop_cols, axis = 1),
                                              test_data.drop(drop_cols, axis = 1), target_feature, categorical_features = cat_cols
                                             )
    ResponsibleAIDashboard(rai_insights, cohort_list=cohort_list)
else:
    pipe = model['DT'][:-1]
    try:
        features = pipe.get_feature_names_out()
    except:
        try:
            features = pipe.get_feature_names_out()
            print('Preprocessing - Normal')
        except:
            try:
                p_ind = pipe[-1].get_support(indices = True)
                fn = pipe[0].get_feature_names_out()
                features = [fn[x] for x in p_ind]
                print('Preprocessing - Steps')
            except:
                try:
                    features = get_feature_names(pipe, cat)
                    print('Preprocessing (old) - Normal')
                except:
                    p_ind = pipe[-1].get_support(indices = True)
                    fn = get_feature_names(pipe[0], cat)
                    features = [fn[x] for x in p_ind]
                    print('Preprocessing (old) - Steps')
    pipe.fit(X_train)
    X_test_proc = pd.DataFrame(pipe.transform(X_test), columns=features)
    predictions = model['DT'][-1].predict(X_test_proc)
    ErrorAnalysisDashboard(dataset=X_test_proc, true_y=y_test, features=features, pred_y=predictions, model_task='regression')
```

## Explainer Dashboard

Initialize the dashboard explainer.


```python
# Create and explainer for the dashboard
try:
    explainer = ClassifierExplainer(model['DT'], X_test, y_test) # Input the test set and classifier model here
except:
    explainer = RegressionExplainer(model['DT'], X_test, y_test) # Input the test set and regression model here
```


Run the dashboard.

```python
if reg:
    try:
        ExplainerDashboard(explainer, [
                                    EDATab(explainer, None),
                                    FairnessTab(explainer, model_selected, X_test, y_test, X_train, y_train, test_data, train_data, test_data_proc, train_data_proc, target_feature, model_type),
                                    LocalExpTab(explainer, model_selected, X_train, y_train, X_test,cont, cat, model_type, target_feature, pipe),
                                    GlobalExpTab(explainer, exp, model_selected, X_train, pipe, cat, model_type, variable_groups, features),
                                    StabilityTab(explainer, X_train, y_train, X_test, y_test, cont, pipe, model_selected, train_data, test_data, target_feature, model_type),
                                    StabilityTestTab(explainer, model_selected, train_data, test_data, target_feature, model_type),
                                    RobustnessTab(explainer, model_selected, X_train_proc, y_train, X_test_proc, y_test, model_type),
                                    UncertaintyTab(explainer, model_selected, X_train, y_train, X_test, y_test, model_type),
                                    ], bootstrap = dbc.themes.FLATLY, hide_header = True).run()
    except Exception as e:
        print(e)
elif not reg:
    try:
        ExplainerDashboard(explainer, [
                                EDATab(explainer, None),
                                FairnessTab(explainer, model_selected, X_test, y_test, X_train, y_train, test_data, train_data, test_data_proc, train_data_proc, target_feature, model_type),
                                LocalExpTab(explainer, model_selected, X_train, y_train, X_test,cont, cat, model_type, target_feature, preprocessor),
                                GlobalExpTab(explainer, exp, model_selected, X_train, preprocessor, cat, model_type, variable_groups, features),
                                StabilityTab(explainer, X_train, y_train, X_test, y_test, cont, preprocessor, model_selected, train_data, test_data, target_feature, model_type),
                                StabilityTestTab(explainer, model_selected, train_data, test_data, target_feature, model_type),
                                RobustnessTab(explainer, model_selected, X_train_proc, y_train, X_test_proc, y_test, model_type),
                                UncertaintyTab(explainer, model_selected, X_train, y_train, X_test, y_test, model_type),
                                ], bootstrap = dbc.themes.FLATLY, hide_header = True).run()
    except Exception as e:
        print(e)
```

This will generate a local link that you can use to run the dashboard on a browser. Below is a short gif that showcases what the dashboard should look like upon running.

<!-- <p align="center">
  <img src="../../assets/images/XRAI_Teaser - shortened.gif">
</p> -->

![](../../assets/images/XRAI_Teaser - shortened.gif)