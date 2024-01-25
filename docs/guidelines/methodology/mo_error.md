---
layout: default
title: M&O - Error Analysis
parent: XRAI Methodology
grand_parent: Guidelines
nav_order: 4
---

# XRAI Methodology - Model & Output (M&O) - Error Analysis
{: .no_toc }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}
**
Error analysis in the context of machine learning involves closely examining the errors made by a trained model to gain insights into its performance, identify patterns, and inform improvements. By analyzing the types of errors the model is making, you can better understand its strengths and weaknesses, and potentially take corrective actions to enhance its predictive capabilities. 

## Classification 
Error analysis techniques for classification problems aim to understand the types of errors a model is making and provide insights into its performance. Here are several common error analysis techniques used in the context of classification: 

1. **Confusion Matrix Analysis**: A confusion matrix is a table that summarizes the performance of a classification model. It shows the true positive, true negative, false positive, and false negative counts for each class. From the confusion matrix, you can calculate metrics like accuracy, precision, recall, and F1-score to assess different aspects of the model's performance. 
    - Using scikit-learn: This module provides convenient functions to compute the confusion matrix.

    ```python
    from sklearn.metrics import confusion_matrix, classification_matrix
    from sklearn.model_selection import train_test_split
    from sklearn.svm import SVC

    X_train, X_test, y_train, y_test = train_test_split(X, y, test_size = 0.2, random_state = 42)
    model = SVC()
    model.fit(X_train, y_train)

    # Make predictions
    y_pred = model.predict(X_test)

    # Compute confusion matrix
    cm = confusion_matrix(y_test, y_pred)
    print('Confusion Matrix:\n', cm)

    # Additional metrics
    print('Classification Report:\n', classification_report(y_test, y_pred))
    ```

    - Using Yellowbrick: It's a visualization library for machine learning that includes a ConfusionMatrix visualizer.

    ```python
    from yellowbrick.classifier import ConfusionMatrix

    # Visualize confusion matrix using Yellowbrick
    cm_visualizer = ConfusionMatrix(model)
    cm_visualizer.score(X_test, y_test)
    cm_visualizer.show()
    ```

    - Custom function: You can create your own function to print the confusion matrix.

    ```python
    def custom_cm(y_true, y_pred, labels):
        cm = pd.crosstab(pd.Series(y_true, name = 'Actual'), pd.Series(y_pred, name = 'Predicted'))
        return cm
    ```

2. **ROC Curve and AUC Analysis**: The Receiver Operating Characteristic (ROC) curve is a graphical representation of a model's trade-off between true positive rate and false positive rate at different classification thresholds. The Area Under the ROC Curve (AUC) summarizes the overall performance of the model. ROC analysis helps you visualize how the model's sensitivity and specificity change with different threshold settings. 
    - Using scikit-learn: It provides functions for computing ROC curve and AUC.

    ```python
    from sklearn.metrics import roc_curve, auc, roc_auc_score
    import matplotlib.pyplot as plt

    # Obtain predicted probabilities
    y_prob = model.predict_proba(X_test)[:, 1]

    # Compute ROC curve and AUC
    fpr, tpr, thresholds = roc_curve(y_test, y_prob)
    roc_auc = auc(fpr, tpr)

    # You can also directly compute AUC
    auc_score = roc_auc_score(y_test, y_prob)

    # Plot ROC curve
    plt.figure(figsize = (8, 6))
    plt.plot(fpr, tpr, color = 'orange', lw = 2, label = f'AUC = {roc_auc:.4f}')
    plt.plot([0, 1], [0, 1], color = 'blue', lw = 2, linestyle = '--')
    plt.xlabel('False Positive Rate')
    plt.ylabel('True Positive Rate')
    plt.title('ROC Curve')
    plt.legend(loc = 'lower right')
    plt.show()
    ```

    - Using scikit-plot: An alternative module that simplifies the process of creating ROC curves.

    ```python
    import scikitplot as skplt

    # Plot ROC curves using scikit-plot
    skplt.metrics.plot_roc_curve(y_test, y_prob)
    plt.show()
    ```

    - Using Yellowbrick: This module also contains an ROC-AUC visualizer.

    ```python
    from yellowbrick.classifier import ROCAUC

    model = SVC(probability = True)
    # Visualize ROC-AUC with Yellowbrick
    roc_auc_visualizer = ROCAUC(model)
    roc_auc_visualizer.score(X_test, y_test)
    roc_auc_visualizer.show()
    ```

3. **Precision-Recall Curve Analysis**: Similar to the ROC curve, the Precision-Recall curve shows the trade-off between precision and recall for different classification thresholds. It's particularly useful when dealing with imbalanced datasets where one class is much more frequent than the other. 
    - Using scikit-learn: It provides functions for computing ROC curve and AUC.

        ```python
        from sklearn.metrics import precision_recall_curve, average_precision_scores
        import matplotlib.pyplot as plt

        # Obtain predicted probabilities
        y_prob = model.predict_proba(X_test)[:, 1]

        # Compute Precision-Recall Curve
        precision, recall, _ = precision_recall_curve(y_test, y_prob)

        # Compute average precision
        avg_precision = average_precision_score(y_test, y_prob)

        # Plot ROC curve
        plt.figure(figsize = (8, 6))
        plt.plot(recall, precision, color = 'orange', lw = 2, label = f'AUC = {avg_precision:.4f}')
        plt.plot([0, 1], [0, 1], color = 'blue', lw = 2, linestyle = '--')
        plt.xlabel('Recall')
        plt.ylabel('Precision')
        plt.title('PR Curve')
        plt.legend(loc = 'lower right')
        plt.show()
        ```

        - Using scikit-plot: An alternative module that simplifies the process of creating ROC curves.

        ```python
        # Plot PR curves using scikit-plot
        skplt.metrics.plot_precision_recall_curve(y_test, y_prob)
        plt.show()
        ```

        - Using Yellowbrick: This module also contains an ROC-AUC visualizer.

        ```python
        from yellowbrick.classifier import PrecisionRecallCurve

        model = SVC(probability = True)
        # Visualize PR Curve with Yellowbrick
        roc_auc_visualizer = PrecisionRecallCurve(model)
        roc_auc_visualizer.score(X_test, y_test)
        roc_auc_visualizer.show()
        ```
4. **Class-wise Error Analysis**: Instead of looking at overall metrics, analyze the performance of the model for each individual class. Identify which classes are being predicted accurately and which ones have the most errors. This is especially important in multi-class classification tasks. 
    - Using scikit-learn's `classification_report` and `confusion_matrix`: Like with binary classes, these can also be used for multi-class reports.

    ```python
    # Generate classification report
    report = classification_report(y_test, y_pred, target_names = class_names, output_dict = True)

    # Convert to pandas DataFrame for class-wise analysis
    class_wise_analysis = pd.DataFrame(report).transpose()

    # Generate confusion matrix
    cm = confusion_matrix(y_test, y_pred)

    # Extract class-wise metrics from confusion matrix
    class_wise_metrics = {"Class": class_names, "Precision": [], "Recall": [], "F1-Score": []}
    for i in range(len(class_names)):
        precision = cm[i, i] / cm[:, i].sum()
        recall = cm[i, i] / cm[i, :].sum()
        f1_score = 2 * (precision * recall) / (precision + recall)

        class_wise_metrics["Precision"].append(precision)
        class_wise_metrics["Recall"].append(recall)
        class_wise_metrics["F1-Score"].append(f1_score)

    class_wise_analysis = pd.DataFrame(class_wise_metrics)
    ```

    - Using scikit-learn's `precision_recall_fscore_support`: An alternative report that provides scores for each class.

    ```python
    from sklearn.metrics import precision_recall_fscore_support

    # Get precision, recall, and F1-score for each class
    metrics_per_class = precision_recall_fscore_support(y_test, y_pred, labels = class_names)

    # Create a DataFrame for class-wise analysis
    class_wise_analysis = pd.DataFrame({
        'Class': class_names,
        'Precision': metrics_per_class[0],
        'Recall': metrics_per_class[1],
        'F1-Score': metrics_per_class[2],
        'Support': metrics_per_class[3]
    })
    ```

    - Using Yellowbrick: Yellowbrick also has its own visualizer for detailed class-wise analysis.

    ```python
    from yellowbrick.classifier import ClassificationReport

    # Visualize class-wise metrics with Yellowbrick
    class_report_visualizer = ClassificationReport(model, support = True, cmap = 'viridis')
    class_report_visualizer.score(X_test, y_test)
    class_report_visualizer.show()
    ```

5. **Misclassification Analysis**: Examine the specific instances that were misclassified by the model. Analyze their features, patterns, and context to identify common factors contributing to the errors. This can provide insights into areas where the model might need improvement. 
6. **Feature Importance Analysis**: If your model provides feature importance scores, analyze which features contribute the most to correct or incorrect predictions. This can help you identify which features are more influential in the decision-making process. 
    - Using model feature importance methods: Models like XGBoost and scikit-learn's RandomForest provide natural ways of computing feature importance.

    ```python
    from sklearn.ensemble import RandomForestClassifier
    from sklearn.linear_model import Lasso
    import xgboost as xgb
    import matplotlib.pyplot as plt

    # Random Forest
    model = RandomForestClassifier()
    model.fit(X_train, y_train)

    # XGBoost
    model = xgb.XGBClassifier()
    model.fit(X_train, y_train)

    # Lasso
    model = Lasso(alpha=0.01)
    model.fit(X_train, y_train)

    # Get feature importances
    feature_importances = model.feature_importances_

    # Visualize feature importances
    plt.barh(range(len(feature_importances)), feature_importances, align='center')
    plt.yticks(range(len(feature_importances)), feature_names)
    plt.xlabel('Feature Importance')
    plt.ylabel('Feature')
    plt.show()
    ```

    - Using permutation importance: This measures the change in model performance when feature values are randomly permuted.

    ```python
    from sklearn.inspection import permutation_importance

    # Example: Obtaining permutation importances
    result = permutation_importance(model, X_test, y_test, n_repeats=10, random_state=42)

    # Get feature importances
    feature_importances = result.importances_mean

    # Visualize feature importances
    plt.barh(range(len(feature_importances)), feature_importances, align='center')
    plt.yticks(range(len(feature_importances)), feature_names)
    plt.xlabel('Permutation Importance')
    plt.ylabel('Feature')
    plt.show()
    ```

    - Using SHAP (SHapley Additive exPlanations): SHAP values provide a unified measure of feature importance, and can be used for a wide range of models.

    ```python
    import shap

    # Example: Creating a SHAP explainer
    explainer = shap.Explainer(model)
    shap_values = explainer.shap_values(X_test)

    # Visualize SHAP summary plot
    shap.summary_plot(shap_values, X_test, feature_names=feature_names)
    ```

7. **Error Visualization**: Create visualizations to represent errors, such as confusion matrices, heatmaps, or scatter plots. These visuals can help you quickly identify patterns and trends in the errors. 
8. **Cross-Validation Analysis**: Perform cross-validation to assess the model's performance across different folds of the data. This helps ensure that the model's performance is consistent and not influenced by particular subsets of the data.
    - K-Fold Cross Validation: We can perform k-fold cross-validation, ensuring that each fold has a similar distribution of target classes.

    ```python
    from sklearn.model_selection import StratifiedKFold, RepeatedStratifiedKFold, cross_val_score
    
    model = RandomForestClassifier()

    # Stratified K-Fold - maintains class distribution in each fold
    kfold = StratifiedKFold(n_splits=5, shuffle=True, random_state=42)
    cv_scores = cross_val_score(model, X, y, cv=kfold, scoring='accuracy')

    # Repeated Stratified K-Fold - repeatedly uses different random seeds for k-fold splits
    rkfold = RepeatedStratifiedKFold(n_splits=5, n_repeats=3, random_state=42)
    cv_scores = cross_val_score(model, X, y, cv=rkfold, scoring='accuracy')
    ```

    - Leave-One-Out Cross-Validation (LOOCV): Each observation is used as a test set exactly once.

    ```python
    from sklearn.model_selection import LeaveOneOut

    loo = LeaveOneOut()
    cv_scores = cross_val_score(model, X, y, cv=loo, scoring='accuracy')
    ```

    - Stratified Shuffle Split: Useful when dealing with imbalanced datasets, as it maintains class distribution in each split.

    ```python
    from sklearn.model_selection import StratifiedShuffleSplit

    sss = StratifiedShuffleSplit(n_splits=5, test_size=0.2, random_state=42)
    cv_scores = cross_val_score(model, X, y, cv=sss, scoring='accuracy')
    ```

9. **Threshold Analysis**: Examine how different classification thresholds impact the model's performance. Changing the threshold can influence metrics like precision and recall, which might be more suitable depending on the problem.  
10. **Sample Analysis**: If misclassifications are based on specific samples, analyze those samples in detail. This could involve domain-specific expertise to understand why certain samples are challenging to classify. 

## Regression 
Error analysis techniques for regression problems involve evaluating and understanding the performance of regression models. Here are several common error analysis techniques used in the context of regression: 

1. **Mean Squared Error (MSE) and Root Mean Squared Error (RMSE) Analysis**: MSE measures the average squared difference between predicted and actual values. RMSE is the square root of MSE, providing a more interpretable metric. Lower values indicate better performance. 
    - Using scikit-learn: Scikit-learn provides functions to compute both metrics.

    ```python
    from sklearn.metrics import mean_squared_error

    y_true = np.array([1, 2, 3, 4, 5])
    y_pred = np.array([1.5, 2.5, 3.5, 4.5, 5.5])

    mse = mean_squared_error(y_true, y_pred)
    rmse = np.sqrt(mse)

    print("Mean Squared Error:", mse)
    print("Root Mean Squared Error:", rmse)
    ```

    - Using NumPy: You can also manually compute these metrics with NumPy.

    ```python
    mse = ((y_true - y_pred) ** 2).mean()
    rmse = np.sqrt(mse)

    print("Mean Squared Error:", mse)
    print("Root Mean Squared Error:", rmse)
    ```

2. **Mean Absolute Error (MAE) Analysis**: MAE measures the average absolute difference between predicted and actual values. It is less sensitive to outliers than MSE. 
    - Using scikit-learn: It provides a function to calculate MAE.

    ```python
    from sklearn.metrics import mean_absolute_error

    mae = mean_absolute_error(y_true, y_pred)
    print("Mean Absolute Error:", mae)
    ```

    - Using NumPy: You can manually compute MAE with NumPy.

    ```python
    mae = np.abs(y_true - y_pred).mean()
    print("Mean Absolute Error:", mae)
    ```

3. **R-squared (Coefficient of Determination) Analysis**: R-squared measures the proportion of the variance in the dependent variable that is predictable from the independent variables. It provides insight into how well the model fits the data. 
    - Using scikit-learn: It provides a function to compute R-squared. It can also be done via `linear_model`.

    ```python
    from sklearn.metrics import r2_score
    from sklearn.linear_model import LinearRegression

    r2 = r2_score(y_true, y_pred)
    print("R-squared:", r2)

    y_true = np.array([1, 2, 3, 4, 5])
    X = np.arange(1, 6).reshape(-1, 1)

    model = LinearRegression().fit(X, y_true)
    r2_sklearn = model.score(X, y_true)

    print("R-squared (scikit-learn LinearRegression):", r2_sklearn)
    ```

    - Using statsmodels: Useful for estimating statistical models, providing more detailed outputs.

    ```python
    import statsmodels.api as sm

    y_true = np.array([1, 2, 3, 4, 5])
    X = sm.add_constant(np.arange(1, 6))
    model = sm.OLS(y_true, X).fit()

    r2_statsmodels = model.rsquared

    print("R-squared (Statsmodels):", r2_statsmodels)
    ```

    - Using NumPy: You can manually compute R-squared with NumPy.

    ```python
    y_true = np.array([1, 2, 3, 4, 5])
    y_pred = np.array([1.5, 2.5, 3.5, 4.5, 5.5])

    mean_y_true = np.mean(y_true)
    ss_total = np.sum((y_true - mean_y_true) ** 2)
    ss_residual = np.sum((y_true - y_pred) ** 2)

    r2_manual = 1 - (ss_residual / ss_total)

    print("R-squared (Manual):", r2_manual)
    ```

    - Using SciPy: SciPy offers a wide range of scientific computing functionality, which includes computing for R-squared.

    ```python
    from scipy.stats import linregress

    slope, intercept, r_value, p_value, std_err = linregress(y_pred, y_true)
    r2 = r_value ** 2

    print("R-squared (Scipy):", r2)
    ```
    
4. **Residual Analysis**: Examine the distribution of residuals (differences between predicted and actual values). Visualizations like residual plots, histogram of residuals, and Q-Q plots can help identify patterns and potential issues like heteroscedasticity.
    - Residual Plots: We can visualize residuals with scatter plots and check for homoscedasticity.

    ```python
    residuals = y_true - y_pred

    # Scatter plot of residuals
    plt.scatter(y_pred, residuals)
    plt.axhline(y=0, color='red', linestyle='--', linewidth=2)
    plt.xlabel('Predicted Values')
    plt.ylabel('Residuals')
    plt.title('Residual Plot')
    plt.show()

    # Residuals distribution plot
    sns.histplot(residuals, kde=True)
    plt.xlabel('Residuals')
    plt.ylabel('Frequency')
    plt.title('Residuals Distribution Plot')
    plt.show()
    ```

    - Quantile-Quantile (Q-Q) Plot: We can check if the residuals follow a normal distribution.

    ```python
    from scipy.stats import probplot

    probplot(residuals, plot = plt)
    plt.title('Q-Q Plot of Residuals')
    plt.show()
    ```

    - Leverage-Residual Plot: Identifying influential observation with leverage-residual plots.

    ```python
    from statsmodels.graphics.regressionplots import plot_leverage_resid2

    plot_leverage_resid2(results)
    plt.title('Leverage-Residual Plot')
    plt.show()
    ```

    - Residuals vs. Fitted Values Plot: Examine the relationship between residuals and fitted values.

    ```python
    plt.scatter(y_pred, residuals)
    plt.axhline(y=0, color='red', linestyle='--', linewidth=2)
    plt.xlabel('Fitted Values')
    plt.ylabel('Residuals')
    plt.title('Residuals vs. Fitted Values Plot')
    plt.show()
    ```

    - Cook's Distance Plot: Assessing the influence of each observation on the model using Cook's distance.

    ```python
    from statsmodels.stats.outliers_influence import OLSInfluence

    influence = OLSInfluence(results)
    cooks_distance = influence.cooks_distance

    plt.stem(cooks_distance, basefmt=" ", markerfmt=",", linefmt="r-")
    plt.xlabel('Observation Index')
    plt.ylabel("Cook's Distance")
    plt.title("Residual Analysis - Cook's Distance Plot")
    plt.show()
    ```

    - Durbin-Watson Statistic: Check for autocorrelation in residuals using the Durbin-Watson statistic:

    ```python
    from statsmodels.stats.stattools import durbin_watson

    dw_statistic = durbin_watson(residuals)
    print("Durbin-Watson Statistic:", dw_statistic)
    ```

5. **Feature Importance Analysis**: If your regression model provides feature importance scores, analyze which features contribute the most to the prediction. This helps you understand which features have the greatest influence on the outcome. 
6. **Cross-Validation Analysis**: Perform cross-validation to assess how well the model generalizes to unseen data. Variability in performance across different folds can help you evaluate model stability. 
7. **Prediction Interval Analysis**: Estimate prediction intervals around the predicted values to quantify the uncertainty of predictions. This is especially important when interpreting regression models in real-world scenarios. 
    - Bootstrapping: Use bootstrap resampling to estimate the prediction interval.

    ```python
    from sklearn.utils import resample

    n_iterations = 1000
    predictions = []

    for _ in range(n_iterations):
        X_boot, y_boot = resample(X, y)
        model.fit(X_boot, y_boot)
        y_pred_boot = model.predict(X_new)
        predictions.append(y_pred_boot)

    prediction_interval = np.percentile(predictions, [2.5, 97.5], axis=0)
    ```

    - Statsmodels with Confidence Intervals: This library enables you to calculate the confidence intervals for predictions.

    ```python
    X = sm.add_constant(X)  # Add a constant term for the intercept
    model = sm.OLS(y, X).fit()

    # Create new data for prediction
    new_data = sm.add_constant(np.array([[1, 10], [1, 15], [1, 20]]))

    # Get predictions and prediction intervals
    pred_results = model.get_prediction(new_data)
    pred_intervals = pred_results.conf_int(alpha=0.05)  # 95% confidence interval

    print("Predicted Values:", pred_results.predicted_mean)
    print("Prediction Intervals:")
    print(pred_intervals)
    ```

    - Bayesian Inference: We can do Bayesian modeling with PyMC3.

    ```python
    import pymc3 as pm

    with pm.Model() as model:
        alpha = pm.Normal('alpha', mu=0, sd=10)
        beta = pm.Normal('beta', mu=0, sd=10)
        sigma = pm.HalfNormal('sigma', sd=1)

        mu = alpha + beta * X
        y_obs = pm.Normal('y_obs', mu=mu, sd=sigma, observed=y)

        trace = pm.sample(1000, tune=1000)

    # Extract prediction samples
    y_pred_samples = pm.sample_posterior_predictive(trace, samples=1000)['y_obs']
    prediction_interval = np.percentile(y_pred_samples, [2.5, 97.5], axis=0)
    ```

    - Monte Carlo Simulation: Conduct a Monte Carlo simulation to estimate prediction intervals.

    ```python
    num_simulations = 1000
    simulation_predictions = np.zeros((len(X_test), num_simulations))

    for i in range(num_simulations):
        # Simulate new data points based on model uncertainty
        simulated_data = np.random.normal(loc=model.predict(X_test), scale=model.resid.std())
        simulation_predictions[:, i] = simulated_data

    # Calculate percentiles for lower and upper bounds
    lower_bounds_mc = np.percentile(simulation_predictions, 2.5, axis=1)
    upper_bounds_mc = np.percentile(simulation_predictions, 97.5, axis=1)

    print("Lower bounds of prediction interval (Monte Carlo):", lower_bounds_mc)
    print("Upper bounds of prediction interval (Monte Carlo):", upper_bounds_mc)
    ```

8. **Heteroscedasticity Analysis**: Check for heteroscedasticity, which is the non-constant variance of residuals across the range of predicted values. Heteroscedasticity can impact the model's reliability. 
    - Goldfeld-Quandt Test: This tests for heteroscedasticity by comparing the variance of residuals in different segments of data.

    ```python
    from statsmodels.stats.diagnostic import het_goldfeldquandt

    _, p_value, _ = het_goldfeldquandt(y_true - y_pred, X)
    print("Goldfeld-Quandt Test p-value:", p_value)
    ```

    - Breusch-Pagan Test: This is another test for heteroscedasticity.

    ```python
    from statsmodels.stats.diagnostic import het_breuschpagan

    _, p_value, _, _ = het_breuschpagan(model.resid, model.model.exog)
    print("Breusch-Pagan Test p-value:", p_value)
    ```

    - White's Test: This is a general test for heteroscedasticity.

    ```python
    from statsmodels.stats.diagnostic import het_white

    _, p_value, _, _ = het_white(residuals, exog=X)
    print("White's Test p-value:", p_value)
    ```

    - Barlett's Test: This is used to test for homogeneity of variances.

    ```python
    from scipy.stats import bartlett

    _, p_value = bartlett(model.resid, fitted_values)
    print("Barlett's Test p-value:", p_value)
    ```

    - Levene's Test: This is a non-paramtric test for the equality of variances.

    ```python
    from scipy.stats import levene

    _, p_value = levene(model.resid, fitted_values)
    print("Levene's Test p-value:", p_value)
    ```

    - ARCH and GARCH Models: Autoregressive Conditional Heteroscedasticity (ARCH) and Generalized ARCH (GARCH) models are used for modeling time-varying volatility in time series data.

    ```python
    from arch import arch_model

    model = arch_model(residuals)
    results = model.fit()

    print(results.summary())
    ```

9. **Leverage and Influence Analysis**: Identify data points with high leverage and influence. These points can disproportionately affect the regression model's fit and coefficients. 
    - Difference in Fits (DFFITS): This measures the change in predicted values when an observation is omitted.

    ```python
    influence = OLSInfluence(model)
    dffits = influence.dffits

    plt.stem(dffits, basefmt=" ", markerfmt=",", linefmt="r-")
    plt.xlabel('Observation Index')
    plt.ylabel('DFFITS')
    plt.title('DFFITS Analysis')
    plt.show()
    ```

    - Difference in Betas (DFBETAS): This measures the change in regression coefficients when an observation is omitted.

    ```python
    influence = OLSInfluence(model)
    dfbetas = influence.dfbetas

    for i, coefficient in enumerate(model.params):
        plt.stem(dfbetas[:, i], basefmt=" ", markerfmt=",", linefmt="r-")
        plt.xlabel('Observation Index')
        plt.ylabel(f'DFBETAS for coefficient {i}')
        plt.title(f'DFBETAS Analysis - Coefficient {i}')
        plt.show()
    ```

    - Hat Matrix Diagonal Values: This examines the diagonal values of the hat matrix (leverage values).
    
    ```python
    influence = OLSInfluence(model)
    hat_matrix_diag = influence.hat_matrix_diag

    plt.stem(hat_matrix_diag, basefmt=" ", markerfmt=",", linefmt="r-")
    plt.xlabel('Observation Index')
    plt.ylabel('Hat Matrix Diagonal Values')
    plt.title('Hat Matrix Diagonal Values Analysis')
    plt.show()
    ```

    - Influence Plot: This shows standardizes residuals against leverage values.

    ```python
    from statsmodels.graphics.regressionplots import influence_plot

    influence_plot(results)
    plt.title('Influence Plot')
    plt.show()
    ```

10. **Collinearity Analysis**: Assess multicollinearity among predictor variables. Highly correlated predictors can lead to unstable coefficient estimates and reduced model interpretability. 
    - Variance Inflation Factor (VIF): Checking for multicollinearity by examining VIF values.

    ```python
    from statsmodels.stats.outliers_influence import variance_inflation_factor

    vif_values = [variance_inflation_factor(X.values, i) for i in range(X.shape[1])]
    vif_df = pd.DataFrame({'Variable': X.columns, 'VIF': vif_values})

    print(vif_df)
    ```

    - Condition Number: This measures the sensitivity of a regression coefficient to small changes in the data.

    ```python
    from numpy.linalg import cond

    condition_number = cond(X)
    print("Condition Number:", condition_number)
    ```

    - Tolerance and Variance Proportions: Tolerance is the reciprocal of VIF, and variance proportions represent the proportion of variance of each variable that is not explained by other predictors. Vari

    ```python
    vif_data = X.copy()
    vif_data['Intercept'] = 1  # Add intercept column

    tolerance = 1 / np.array([variance_inflation_factor(vif_data.values, i) for i in range(vif_data.shape[1])])
    variance_proportions = 1 - tolerance

    print("Tolerance:")
    print(tolerance)
    print("\nVariance Proportions:")
    print(variance_proportions)
    ```

    - Eigenvalues and Eigenvectors: Analyze the eigenvalues and eigenvectors of the correlation matrix to provide insights into collinearity

    ```python
    correlation_matrix = X.corr()
    eigenvalues, eigenvectors = np.linalg.eig(correlation_matrix)

    print("Eigenvalues:")
    print(eigenvalues)
    print("\nEigenvectors:")
    print(eigenvectors)
    ```

    - Principal Component Analysis (PCA): PCA can be used to transform the original features into uncorrelated PCs, revealing collinearity patterns.

    ```python
    from sklearn.decomposition import PCA

    pca = PCA()
    pca.fit(X)

    explained_variance_ratio = pca.explained_variance_ratio_
    principal_components = pca.components_

    print("Explained Variance Ratio:")
    print(explained_variance_ratio)
    print("\nPrincipal Components:")
    print(principal_components)
    ```

## Clustering 
Error analysis techniques for clustering or segmentation problems involve evaluating and understanding the performance of clustering algorithms, which group data points into clusters based on their similarity. Here are several common error analysis techniques used in the context of clustering: 

1. **Silhouette Score Analysis**: The silhouette score measures how close each data point in one cluster is to the data points in the neighboring clusters. Higher silhouette scores indicate better-defined clusters. 
    - Scikit-learn's `silhouette_score`: This function computes the average silhouette score for a set of samples. 

    ```python
    from sklearn.metrics import silhouette_score
    from sklearn.cluster import KMeans
    from sklearn.datasets import make_blobs

    X, y = make_blobs(n_samples=300, centers=4, random_state=42)
    kmeans = KMeans(n_clusters=4, random_state=42)
    labels = kmeans.fit_predict(X)

    silhouette_avg = silhouette_score(X, labels)
    print("Silhouette Score:", silhouette_avg)
    ```

    - Yellowbrick: This library provides a `SilhouetteVisualizer` for a visual representation of silhouette scores.

    ```python
    from yellowbrick.cluster import SilhouetteVisualizer

    visualizer = SilhouetteVisualizer(kmeans)
    visualizer.fit(X)
    visualizer.show()
    ```

    - Scikit-learn's `silhouette_samples`: This provides silhouette scores for each data point.

    ```python
    from sklearn.metrics import silhouette_samples

    silhouette_values = silhouette_samples(X, labels)

    print("Silhouette Scores for each data point:")
    print(silhouette_values)
    ```

    - With NumPy: We can compute silhouette scores manually with NumPy.

    ```python
    from sklearn.metrics import pairwise_distances
    import numpy as np

    def silhouette_score_custom(X, labels):
        distances = pairwise_distances(X)
        num_samples = len(X)

        silhouette_values = []

        for i in range(num_samples):
            a_i = np.mean([distances[i, j] for j in range(num_samples) if labels[i] == labels[j] and i != j])
            b_i = min([np.mean([distances[i, k] for k in range(num_samples) if labels[j] == labels[k]]) for j in range(num_samples) if labels[i] != labels[j]])

            silhouette_i = (b_i - a_i) / max(a_i, b_i)
            silhouette_values.append(silhouette_i)

        silhouette_avg = np.mean(silhouette_values)
        return silhouette_avg

    silhouette_avg_custom = silhouette_score_custom(X, labels)
    print("Custom Silhouette Score:", silhouette_avg_custom)
    ```

2. **Inertia (Within-Cluster Sum of Squares) Analysis**: Inertia quantifies the total squared distance between each data point and its cluster center. Lower inertia suggests tighter and more compact clusters.
    - `inertia_` attribute: Most clustering algorithms in scikit-learn have the `inertia_` attribute, allowing you to retrieve the inertia after fitting the model.

    ```python
    from sklearn.cluster import KMeans

    kmeans = KMeans(n_clusters=3, random_state=42)
    kmeans.fit(X)

    inertia = kmeans.inertia_
    print("Inertia:", inertia)
    ```

    - Elbow Method: Plot the inertia for different numbers of clusters to choose the optimal number.

    ```python
    range_n_clusters = [2, 3, 4, 5, 6]

    inertias = []
    for n_clusters in range_n_clusters:
        kmeans = KMeans(n_clusters=n_clusters, random_state=42)
        kmeans.fit(X)
        inertias.append(kmeans.inertia_)

    plt.plot(range_n_clusters, inertias, marker='o')
    plt.xlabel('Number of Clusters')
    plt.ylabel('Inertia')
    plt.title('Elbow Method for Inertia Analysis')
    plt.show()
    ```

    - Yellowbrick: This library provides a visualizer for the elbow method.

    ```python
    from yellowbrick.cluster import KElbowVisualizer

    # Example: Elbow method using yellowbrick
    model = KMeans()
    visualizer = KElbowVisualizer(model, k=(2, 6))

    visualizer.fit(X)  # Fit the data to the visualizer
    visualizer.poof()  # Draw/show/poof the data
    ```

    - With NumPy: Implement a custom inertia calculation based on the formula.

    ```python
    def inertia_custom(X, labels, centroids):
        distances = pairwise_distances(X, centroids)
        n = len(X)
        inertia_value = 0

        for i in range(n):
            cluster_idx = labels[i]
            inertia_value += distances[i, cluster_idx] ** 2

        return inertia_value

    centroids = kmeans.cluster_centers_
    inertia_custom_value = inertia_custom(X, cluster_labels, centroids)
    print("Custom Inertia:", inertia_custom_value)
    ```

3. **Davies-Bouldin Index Analysis**: This index measures the average similarity between each cluster and its most similar cluster. Lower values indicate better-defined clusters. 
    - Using scikit-learn: The library provides a function specifically for computing the DBI.

    ```python
    from sklearn.metrics import davies_bouldin_score

    kmeans = KMeans(n_clusters=3, random_state=42)
    cluster_labels = kmeans.fit_predict(X)

    dbi = davies_bouldin_score(X, cluster_labels)
    print("Davies-Bouldin Index:", dbi)
    ```

    - Using Yellowbrick: We can specify the KElbowVisualizer to utilize the DBI.

    ```python
    visualizer = KElbowVisualizer(model, k=(2, 6), metric='davies_bouldin')

    visualizer.fit(X)  # Fit the data to the visualizer
    visualizer.poof()  # Draw/show/poof the data
    ```

    - With NumPy: We can manually calculate the DBI with NumPy.

    ```python
    def davies_bouldin_index(X, labels, centroids):
        n_clusters = len(np.unique(labels))
        distances = pairwise_distances(centroids, metric='euclidean')
        max_similarity = np.zeros(n_clusters)

        for i in range(n_clusters):
            for j in range(i + 1, n_clusters):
                if i != j:
                    similarity = (np.sum(distances[i, :]) + np.sum(distances[j, :])) / distances[i, j]
                    max_similarity[i] = max(max_similarity[i], similarity)
                    max_similarity[j] = max(max_similarity[j], similarity)

        dbi = np.sum(max_similarity) / n_clusters
        return dbi

    centroids = kmeans.cluster_centers_
    dbi_custom = davies_bouldin_index(X, cluster_labels, centroids)
    print("Custom Davies-Bouldin Index:", dbi_custom)
    ```

4. **Calinski-Harabasz Index Analysis**: This index measures the ratio of between-cluster variance to within-cluster variance. Higher values suggest better-defined clusters. 
    - Using scikit-learn: The library provides a function specifically for computing the CHI.

    ```python
    from sklearn.metrics import calinski_harabasz_score
    
    kmeans = KMeans(n_clusters=3, random_state=42)
    cluster_labels = kmeans.fit_predict(X)

    ch_index = calinski_harabasz_score(X, cluster_labels)
    print("Calinski-Harabasz Index:", ch_index)
    ```

    - Using Yellowbrick: We can specify the KElbowVisualizer to utilize the CHI.

    ```python
    visualizer = KElbowVisualizer(model, k=(2, 6), metric='calinski_harabasz')

    visualizer.fit(X)  # Fit the data to the visualizer
    visualizer.poof()  # Draw/show/poof the data
    ```

    - With NumPy: We can manually calculate the CHI with NumPy.

    ```python
    def calinski_harabasz_index(X, labels, centroids):
        n_samples, n_features = X.shape
        n_clusters = len(np.unique(labels))

        # Compute total mean and within-cluster scatter
        total_mean = np.mean(X, axis=0)
        within_cluster_scatter = np.sum([np.sum((X[labels == i] - centroids[i]) ** 2) for i in range(n_clusters)])

        # Compute between-cluster scatter
        between_cluster_scatter = np.sum([len(labels[labels == i]) * np.sum((centroids[i] - total_mean) ** 2) for i in range(n_clusters)])

        ch_index = (between_cluster_scatter / (n_clusters - 1)) / (within_cluster_scatter / (n_samples - n_clusters))
        return ch_index

    centroids = kmeans.cluster_centers_
    ch_index_custom = calinski_harabasz_index(X, cluster_labels, centroids)
    print("Custom Calinski-Harabasz Index:", ch_index_custom)
    ```

5. **Dendrogram Analysis**: For hierarchical clustering, dendrograms visualize the clustering hierarchy. Analyze the dendrogram to determine the appropriate number of clusters and potential merges. 
    - With SciPy: This function can be used to visualize hierarchical clustering dendrograms.

    ```python
    from scipy.cluster.hierarchy import dendrogram, linkage

    # Perform hierarchical clustering
    linkage_matrix = linkage(X, method='ward')

    # Plot the dendrogram using SciPy
    plt.figure(figsize=(12, 8))
    dendrogram(linkage_matrix, p=5, truncate_mode='level')
    plt.title('Hierarchical Clustering Dendrogram (SciPy)')
    plt.xlabel('Sample Index')
    plt.ylabel('Distance')
    plt.show()
    ```

    - Using `fastcluster`: Use this li9brary for a faster implementation of hierarchical clustering.

    ```python
    from fastcluster import linkage
    
    linkage_matrix = linkage(X, method='ward')

    plt.figure(figsize=(12, 6))
    dendrogram(linkage_matrix, color_threshold=0, leaf_font_size=8)
    plt.title('Hierarchical Clustering Dendrogram (FastCluster)')
    plt.xlabel('Sample Index')
    plt.ylabel('Distance')
    plt.show()
    ```

    - Using Plotly: This provides interactive dendrograms.

    ```python
    from plotly.figure_factory import create_dendrogram
    import plotly.graph_objects as go

    dendrogram_fig = create_dendrogram(X, orientation='right', labels=list(range(len(X))))
    dendrogram_fig.update_layout(width=800, height=500)
    dendrogram_fig.show()
    ```

    - Using HDBSCAN: This is a clustering library that includes hierarchical clustering and dendrogram plotting capabilities.

    ```python
    import hdbscan
    
    clusterer = hdbscan.HDBSCAN(metric='euclidean', min_cluster_size=5)
    clusterer.fit(X)

    clusterer.condensed_tree_.plot(cmap='viridis', colorbar=True, label_clusters=True)
    plt.title('HDBSCAN Dendrogram')
    plt.xlabel('Sample Index')
    plt.ylabel('Distance')
    plt.show()
    ```

6. **Cluster Profiling**: After clustering, analyze the characteristics of each cluster. Calculate mean, median, or other summary statistics for each feature within each cluster to understand the cluster's properties. 
    - Descriptive Statistics: Calculate the mean, median, standard deviation, and other descriptive statistics for each feature within each cluster. 

    ```python
    cluster_data = pd.DataFrame(X, columns=['Feature1', 'Feature2', 'Feature3'])
    cluster_data['Cluster'] = cluster_labels  # Assign cluster labels to data

    cluster_statistics = cluster_data.groupby('Cluster').describe()
    print(cluster_statistics)
    ```

    - Relative Importance of Features: Evaluate the importance of features within each cluster, which can be helpful for feature selection.

    ```python
    kmeans = KMeans(n_clusters=3, random_state=42)
    cluster_labels = kmeans.fit_predict(X)

    cluster_data = pd.DataFrame(X, columns=['Feature1', 'Feature2', 'Feature3'])
    cluster_data['Cluster'] = cluster_labels

    feature_importance = cluster_data.groupby('Cluster').mean()
    print(feature_importance)
    ```

    - Cluster Sizes and Proportions: Analyze the sizes and proportions of the clusters.

    ```python
    cluster_sizes = cluster_data['Cluster'].value_counts()
    cluster_proportions = cluster_sizes / len(X)

    print("Cluster Sizes:")
    print(cluster_sizes)
    print("\nCluster Proportions:")
    print(cluster_proportions)
    ```

7. **Visual Inspection**: Plot the data points with their assigned cluster labels to visually assess the quality of clustering. Scatter plots, parallel coordinate plots, and heatmaps can reveal cluster patterns.
    - Cluster Centroids: For density-based clustering, you can visualize the cluster centroids to udnerstand the central tendencies of each cluster. 

    ```python
    kmeans = KMeans(n_clusters=3, random_state=42)
    cluster_labels = kmeans.fit_predict(X)
    cluster_centers = kmeans.cluster_centers_

    plt.scatter(X[:, 0], X[:, 1], c=cluster_labels, cmap='viridis')
    plt.scatter(cluster_centers[:, 0], cluster_centers[:, 1], marker='X', s=200, color='red', label='Centroids')
    plt.title('Visualization of Cluster Centroids')
    plt.legend()
    plt.show()
    ```

    - Profile Plots: Create profile plots to visualize the distribution of features within each cluster.

    ```python
    cluster_data = pd.DataFrame(X, columns=['Feature1', 'Feature2', 'Feature3'])
    cluster_data['Cluster'] = cluster_labels

    sns.pairplot(cluster_data, hue='Cluster', palette='viridis')
    plt.suptitle('Profile Plots for Clusters')
    plt.show()
    ```

    - t-SNE Visualization: Use this to visualize clusters in a lower-dimensional space for better interpretability.

    ```python
    tsne = TSNE(n_components=2, random_state=42)
    X_tsne = tsne.fit_transform(X)

    sns.scatterplot(x=X_tsne[:, 0], y=X_tsne[:, 1], hue=cluster_labels, palette='viridis')
    plt.title('t-SNE Visualization of Clusters')
    plt.show()
    ```

    - Using Yellowbrick: The library provides a visualizer for comparing cluster profiles.

    ```python
    from yellowbrick.cluster import ParallelCoordinates

    model = KMeans(n_clusters=3, random_state=42)
    visualizer = ParallelCoordinates(features=['Feature1', 'Feature2', 'Feature3'], normalize='standard')
    visualizer.fit_transform(X, model.fit_predict(X))
    visualizer.show()
    ```

8. **Cluster Stability** Analysis: Perform stability analysis by subsampling the data or perturbing the dataset to assess the stability of cluster assignments. This helps determine if the clusters are reliable and not the result of random fluctuations. 
    - Bootstrapping: This involves generating multiple bootstrap samples from the original dataset and clustering each sample to assess the stability of the resulting clusters.

    ```python
    from sklearn.utils import resample
    
    num_bootstraps = 100
    stability_scores = []

    for _ in range(num_bootstraps):
        bootstrap_sample = resample(X, random_state=42)
        kmeans = KMeans(n_clusters=3, random_state=42)
        cluster_labels = kmeans.fit_predict(bootstrap_sample)
        stability_scores.append(cluster_labels)

    stability_matrix = np.array(stability_scores)
    stability_percentage = np.mean(stability_matrix == mode(stability_matrix, axis=0).mode[0]) * 100
    print(f"Stability Percentage: {stability_percentage:.2f}%")
    ```

    - Subsampling: This involves randomly selecting subset of data and clustering each subset to evaluate the consistency of clusters.

    ```python
    from sklearn.utils import shuffle

    num_subsamples = 100
    stability_scores = []

    for _ in range(num_subsamples):
        subsample = shuffle(X, random_state=42)[:len(X) // 2]
        kmeans = KMeans(n_clusters=3, random_state=42)
        cluster_labels = kmeans.fit_predict(subsample)
        stability_scores.append(cluster_labels)

    stability_matrix = np.array(stability_scores)
    stability_percentage = np.mean(stability_matrix == mode(stability_matrix, axis=0).mode[0]) * 100
    print(f"Stability Percentage (Subsampling): {stability_percentage:.2f}%")
    ```

    - Jaccard Similarity: This measures the similarity between two sets by comparing their intersection and union.

    ```python
    from sklearn.metrics import jaccard_score
    from itertools import combinations

    # Example: Jaccard similarity for stability analysis
    num_clusters = 3
    clusterings = [KMeans(n_clusters=num_clusters, random_state=42).fit_predict(X) for _ in range(num_bootstraps)]

    jaccard_similarities = []
    for pair in combinations(clusterings, 2):
        jaccard_similarity = jaccard_score(pair[0], pair[1], average='micro')
        jaccard_similarities.append(jaccard_similarity)

    stability_score_jaccard = np.mean(jaccard_similarities)
    print(f"Stability Score (Jaccard Similarity): {stability_score_jaccard:.4f}")
    ```

    - Adjusted Rand Index (ARI): This measures the similarity between two clusterings, adjusted for chance.

    ```python
    from sklearn.metrics import adjusted_rand_score

    num_clusters = 3
    clusterings = [KMeans(n_clusters=num_clusters, random_state=42).fit_predict(X) for _ in range(num_bootstraps)]

    ari_scores = []
    for pair in combinations(clusterings, 2):
        ari_score = adjusted_rand_score(pair[0], pair[1])
        ari_scores.append(ari_score)

    stability_score_ari = np.mean(ari_scores)
    print(f"Stability Score (Adjusted Rand Index): {stability_score_ari:.4f}")
    ```

9. **External Validation**: If you have ground-truth labels, use external validation metrics like Adjusted Rand Index (ARI) or Normalized Mutual Information (NMI) to compare the cluster assignments with the true labels. 
    - Normalized Mutual Information (NMI): This measures the mutual information between the true and predicting cluster assignments, normalized by the assignment entropies.

    ```python
    from sklearn.metrics import normalized_mutual_info_score

    kmeans = KMeans(n_clusters=3, random_state=42)
    predicted_labels = kmeans.fit_predict(X)
    true_labels = # Ground truth labels

    nmi = normalized_mutual_info_score(true_labels, predicted_labels)
    print("Normalized Mutual Information:", nmi)
    ```

    - Fowlkes-Mallows Index: This is the geometrix mean of the precision and recall, and is suitable for imbalanced ground truth.

    ```python
    from sklearn.metrics import fowlkes_mallows_score

    kmeans = KMeans(n_clusters=3, random_state=42)
    predicted_labels = kmeans.fit_predict(X)
    true_labels = # Ground truth labels

    fm_index = fowlkes_mallows_score(true_labels, predicted_labels)
    print("Fowlkes-Mallows Index:", fm_index)
    ```

    - Confusion Matrix: This visualizes the agreement and disagreement between true and predicted cluster assignments.

    ```python
    from sklearn.metrics import confusion_matrix
    import seaborn as sns

    kmeans = KMeans(n_clusters=3, random_state=42)
    predicted_labels = kmeans.fit_predict(X)
    true_labels = # Ground truth labels

    cm = confusion_matrix(true_labels, predicted_labels)
    sns.heatmap(cm, annot=True, fmt='d', cmap='Blues')
    plt.xlabel('Predicted Labels')
    plt.ylabel('True Labels')
    plt.title('Confusion Matrix')
    plt.show()
    ```

10. **Overlapping Cluster Analysis**: For algorithms that allow overlapping clusters, analyze the degree of overlap between clusters and identify commonalities between data points assigned to multiple clusters.
    - Fuzzy C-Means (FCM): This allows data points to belong to multiple clusters with varying degrees of membership.

    ```python
    from sklearn.metrics import pairwise_distances_argmin_min
    from sklearn.decomposition import PCA
    from skfuzzy.cluster import cmeans

    # Generate sample data
    np.random.seed(42)
    X = np.concatenate([np.random.normal(loc=i, scale=1, size=(100, 2)) for i in range(3)])

    # Perform Fuzzy C-Means clustering
    n_clusters = 3
    fuzzy_centers, fuzzy_membership, _, _, _, _, _ = cmeans(X.T, c=n_clusters, m=2, error=0.005, maxiter=1000, seed=42)

    # Identify the most probable cluster for each point
    labels, _ = pairwise_distances_argmin_min(X, fuzzy_centers.T)
    membership_values = np.max(fuzzy_membership, axis=0)

    # Visualize the results
    plt.scatter(X[:, 0], X[:, 1], c=labels, cmap='viridis', alpha=0.6)
    plt.title('Fuzzy C-Means Clustering')
    plt.xlabel('Feature 1')
    plt.ylabel('Feature 2')
    plt.show()
    ```

    - Gaussian Mixture Models (GMMs): This models data points as a mixture of multiple Gaussian distributions, allowing for overlapping clusters.

    ```python
    from sklearn.mixture import GaussianMixture

    gmm = GaussianMixture(n_components=3, random_state=42)
    gmm.fit(X)

    labels = gmm.predict(X)

    # Visualize the results
    plt.scatter(X[:, 0], X[:, 1], c=labels, cmap='viridis', alpha=0.6)
    plt.title('Gaussian Mixture Model Clustering')
    plt.xlabel('Feature 1')
    plt.ylabel('Feature 2')
    plt.show()
    ```

    - Affinity Propagation: This allows for the identification of exemplars and assigns data points to multiple clusters.

    ```python
    from sklearn.cluster import AffinityPropagation
    
    X, _ = make_blobs(n_samples=300, centers=3, cluster_std=1.0, random_state=42)

    affinity_propagation = AffinityPropagation(damping=0.9)
    labels = affinity_propagation.fit_predict(X)

    # Visualize the results
    plt.scatter(X[:, 0], X[:, 1], c=labels, cmap='viridis', alpha=0.6)
    plt.title('Affinity Propagation Clustering')
    plt.xlabel('Feature 1')
    plt.ylabel('Feature 2')
    plt.show()
    ```

    - Birch Clustering with Subcluster Assignments: This is a hierarchical clustering algorithm that can assign data points to multiple subclusters within each cluster.

    ```python
    from sklearn.cluster import Birch
    
    X, _ = make_blobs(n_samples=300, centers=3, random_state=42)
    birch = Birch(n_clusters=3)
    birch.fit(X)

    subcluster_assignments = birch.predict(X)
    plt.scatter(X[:, 0], X[:, 1], c=subcluster_assignments, cmap='viridis', alpha=0.7)
    plt.title('Birch Clustering with Subclusters')
    plt.show()
    ```

    - Membership Probability: We can modify traditional density-based clustering algorithms to assign membership probabilities based on distances to cluster centers.

    ```python
    kmeans = KMeans(n_clusters=3, random_state=42)
    kmeans_labels = kmeans.fit_predict(X)

    # Calculate distance to each cluster center
    distances, _ = pairwise_distances_argmin_min(X, kmeans.cluster_centers_)

    # Assign membership probabilities based on distance
    membership_probabilities = 1 / (1 + distances)

    plt.scatter(X[:, 0], X[:, 1], c=membership_probabilities, cmap='viridis', marker='o', edgecolor='black', s=50)
    plt.title('K-Means with Membership Probability')
    plt.xlabel('Feature1')
    plt.ylabel('Feature2')
    plt.show()
    ```
