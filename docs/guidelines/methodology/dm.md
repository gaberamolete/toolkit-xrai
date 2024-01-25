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

Some methods can be used to inspect for model drift. The Kolmogorov-Smirnov test (KS test) which is a nonparametric test, compares the training and post-training data. If the KS test states that the data distributions from both datasets are different, this will confirm the presence of model drift. The other method for drift detection is Page-Hinkley Test by calculating the mean of the observed value and updating the mean when a new data is injected. The drift will be presence when the mean value is greater than the threshold value lambda. 

- Kolmogorov-Smirnov test (KS test): A non-parametric test that checks if the data distributions from both datasets are different.

```python
from scipy.stats import ks_2samp
import numpy as np

def detect_model_drift(training_data, deployment_data):
    stat, p_value = ks_2samp(training_data, deployment_data)
    return p_value

training_data = np.random.normal(0, 1, 1000)
deployment_data = np.random.normal(0.5, 1, 1000)

p_value = detect_model_drift(training_data, deployment_data)
print("KS Test p-value:", p_value)

if p_value < 0.05:
    print("Model drift detected!")
```

- Page-Hinkley Test: Detects model drift in a time-ordered equence of data.

```python
def page_hinkley_test_metrics(data, delta=0.005, min_instances=30):
    mean_values = []
    ph_values = []
    true_positives, false_positives, true_negatives, false_negatives = 0, 0, 0, 0

    for i, value in enumerate(data):
        mean_values.append(value)
        window_size = min(i + 1, min_instances)
        mean_window = np.mean(mean_values[-window_size:])

        if i >= min_instances:
            ph = np.max([0, ph_values[-1] + value - mean_window - delta])
            ph_values.append(ph)

            if ph > delta:
                if i < len(data) - 1 and data[i + 1] > mean_window:
                    true_positives += 1
                else:
                    false_positives += 1
            else:
                if i < len(data) - 1 and data[i + 1] <= mean_window:
                    true_negatives += 1
                else:
                    false_negatives += 1

    sensitivity = true_positives / (true_positives + false_negatives)
    specificity = true_negatives / (true_negatives + false_positives)

    return pd.Series(ph_values, index=data.index), sensitivity, specificity

data = # Load or generate time-ordered data
ph_values, sensitivity, specificity = page_hinkley_test_metrics(data)
```

- Monitoring predictive performance: Monitor the performance of the model on new data.

```python
from sklearn.metrics import accuracy_score
from sklearn.model_selection import train_test_split
from sklearn.ensemble import RandomForestClassifier

X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=42)

model = RandomForestClassifier(n_estimators=100, random_state=42)
model.fit(X_train, y_train)

y_pred = model.predict(X_test)
accuracy = accuracy_score(y_test, y_pred)

print("Accuracy on test data:", accuracy)

if accuracy < threshold:
    print("Model drift detected!")
```

## Check for data drift 
Data drift refers to changes in the distribution of the input features, while the relationship between the features and the target variable remains the same. This means that the statistical properties of the input features change over time, but the underlying concept or meaning of the data remains the same. For example, in a customer churn prediction system, the distribution of customer demographics or transaction data may change over time, leading to a change in the statistical properties of the input features. This can cause the model to become less accurate and may require the model to be retrained or adapted to the new data.  

Data drift can happen when there is a significant gap between the time the data is collected and when the model is used to predict outcomes using real-time data. If this problem is not addressed in a timely manner, this will negatively impact business decisions that were reliant on the model’s predictive capabilities. 

One of the common practices in catching data drifts is by using out-of-time (OOT) testing. OOT testing is the process of testing the model using unforeseen data and inspecting the model’s performance (ie., any decrease in the predictive model performance). A suggested threshold for data drift and retraining is if model performance decreases by more than 15%. However, this threshold value can be selected based on each Data Science team and use case. Furthermore, the Population Stability Index (PSI) or the Characteristics Stability Index (CSI) can be used to quantify the magnitude of the data drift, and these indices can be communicated to the business team that retraining of the model may be required. 

- Population Stability Index (PSI): Used to assess the stability of a population over time, quantifying the distributional changes between two datasets.

```python
def calculate_psi(expected, actual, bins=10):
    expected_bins = np.histogram(expected, bins=bins)[0]
    actual_bins = np.histogram(actual, bins=bins)[0]

    expected_perc = expected_bins / len(expected)
    actual_perc = actual_bins / len(actual)

    psi = np.sum((expected_perc - actual_perc) * np.log(expected_perc / actual_perc))

    return psi

training_data = # Load or generate training data
production_data = # Load or generate production data

psi_score = calculate_psi(training_data['score'], production_data['score'])
print("Population Stability Index (PSI):", psi_score)
```

- Characteristics Stability Index (CSI): Assesses whether the distribution of characteristics remain consistent over time.

```python
def calculate_csi(expected, actual):
    expected_mean = np.mean(expected)
    actual_mean = np.mean(actual)

    expected_std = np.std(expected)
    actual_std = np.std(actual)

    csi = np.abs((expected_mean - actual_mean) / expected_std)

    return csi

training_data = # Load or generate training data
production_data = # Load or generate production data

csi_score = calculate_csi(training_data['feature'], production_data['feature'])
print("Characteristics Stability Index (CSI):", csi_score)
```

- Statistical Metrics: Track statistical metrics of features and compare them over time.

```python
training_data = # Load or generate training data
current_data = # Load or generate current data for prediction

drift_detected = False

for feature in training_data.columns:
    mean_diff = np.abs(training_data[feature].mean() - current_data[feature].mean())
    std_diff = np.abs(training_data[feature].std() - current_data[feature].std())

    if mean_diff > threshold or std_diff > threshold:
        print(f"Drift detected in feature {feature}!")
        drift_detected = True

if not drift_detected:
    print("No data drift detected.")
```

- Categorical Features: Check for changes of categorical features over time.

```python
from sklearn.feature_extraction.text import CountVectorizer
from scipy.spatial.distance import jensenshannon

training_data = # Load or generate training data
current_data = # Load or generate current data for prediction

drift_detected = False

for categorical_feature in ['category', 'label']:
    vectorizer = CountVectorizer()
    X_train = vectorizer.fit_transform(training_data[categorical_feature])
    X_current = vectorizer.transform(current_data[categorical_feature])

    js_distance = jensenshannon(X_train.toarray().flatten(), X_current.toarray().flatten())

    if js_distance > threshold:
        print(f"Drift detected in categorical feature {categorical_feature}!")
        drift_detected = True

if not drift_detected:
    print("No data drift detected.")
```

- Target Distribution: CHeck for changes in the distribution of the target variable over time.

```python
from scipy.stats import chi2_contingency

training_data = # Load or generate training data
current_data = # Load or generate current data for prediction

contingency_table = pd.crosstab(training_data['target'], current_data['target'])
_, p_value, _, _ = chi2_contingency(contingency_table)

if p_value < 0.05:
    print("Drift detected in target variable!")
else:
    print("No data drift detected.")
```

- Outliers: Check for changes in the distribution of outliers over time.

```python
from sklearn.ensemble import IsolationForest

training_data = # Load or generate training data
current_data = # Load or generate current data for prediction

isolation_forest = IsolationForest()
outlier_labels_train = isolation_forest.fit_predict(training_data)
outlier_labels_current = isolation_forest.predict(current_data)

if any(outlier_labels_current == -1):
    print("Data drift detected due to outliers!")
else:
    print("No data drift detected.")
```

## Check for concept drift  
Concept drift refers to changes in the relationship between the input features and the target variable. This means that the underlying concept or meaning of the data changes over time. For example, in a fraud detection system, the types of frauds that are being committed may change over time, leading to a change in the underlying relationship between the features and the target variable. As a result, the model trained on the initial data may become less accurate over time and may need to be retrained or adapted to the new data.  

The same bias metrics during modelling can be used to inspect concept drift. Inspections can be set at frequency selected based on Data Science team and use case (e.g. DDPL bias can be computed every two days, and alert is set if bias metric exceeds confidence interval). 

- Feature Distribution Comparison: Compare the distribution of individual features between training and deployment datasets.

```python
from scipy.stats import wasserstein_distance
def detect_feature_drift(training_feature, deployment_feature):
    distance = wasserstein_distance(training_feature, deployment_feature)
    return distance

training_feature = np.random.normal(0, 1, 1000)
deployment_feature = np.random.normal(0.5, 1, 1000)

distance = detect_feature_drift(training_feature, deployment_feature)
print("Wasserstein Distance:", distance)

if distance > threshold:
    print("Feature drift detected!")
```

- Feature Importance: Keep track of feature importance over time and identify significant changes.

```python
def track_feature_importance(X_train, y_train, X_test, y_test):
    model = RandomForestClassifier(n_estimators=100, random_state=42)
    model.fit(X_train, y_train)

    feature_importances_initial = model.feature_importances_

    model.fit(X_test, y_test)
    feature_importances_current = model.feature_importances_

    return feature_importances_initial, feature_importances_current

feature_importances_initial, feature_importances_current = track_feature_importance(X_train, y_train, X_test, y_test)
```

- Adaptive Windowing (ADWIN): Adopts a sliding window approach to detect any changes in the new data

```python
from skmultiflow.drift_detection import ADWIN

def detect_concept_drift(data_stream):
    adwin = ADWIN()

    for i, data_point in enumerate(data_stream):
        adwin.add_element(data_point)
        if adwin.detected_change():
            print(f"Concept drift detected at position {i}")

data_stream = np.random.normal(0, 1, 1000)
detect_concept_drift(data_stream)
```