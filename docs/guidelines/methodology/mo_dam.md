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
        - Identify missing data: Identify where these missing values are in your dataset.

        ```python
        df = pd.read_csv('dataset.csv')
        print(df.isnull().sum())
        ```
        
        - Remove missing values: There might be rows that have too much missing data, which makes it a unusable data point. Likewise, there might be columns with too much missing data, which also makes it unusable. Remove these corresponding columns and rows.

        ```python
        # Drop rows
        df = df.dropna(thresh = 2) # Keep rows with at least 2 non-NA values

        # Drop columns
        df = df.dropna(subset = ['A', 'B']) # Drop only a subset of columns
        ```

        - Simple Imputation: Fill in missing values with estimated or calculated values. These can usually be the mean, median, or the mode (most frequent) of your data.

        ```python
        # Impute with a constant value
        constant_value = "No Data"
        df = df.fillna(constant_value)

        # Impute with mean
        for col in num_cols:
            df[col] = df[col].fillna(df[col].mean())
        ```

        - Filling: This can be used when missing values follow a pattern, such as time series data. 

        ```python
        # Forward fill
        df = df.ffill()

        # Backward fill
        df = df.bfill()
        ```

        - Interpolation: Use interpolations to estimate missing values based on some surrounding values.

        ```python
        # Polynomial
        df['A'] = df['A'].interpolate(method = 'polynomial', order = 3)

        # Linear
        df['B'] = df['B'].interpolate(method = 'linear', limit_direction = 'backward', axis = 0)
        ```

        - Machine learning-based Imputation: Utilize an ML model (like the `KNNImputer`) to predict missing values based on other dataset features.

        ```python
        from sklearn.impute import KNNImputer

        # KNN imputation
        imputer = KNNImputer(n_neighbors = 5)
        df_knn = pd.DataFrame(imputer.fit_transform(df), columns = df.columns)
        ```

    - **Remove Duplicates**: Identify and remove duplicate records if they exist. 
        - `drop_duplicates`: A very convenient way of removing duplicate rows from a DataFrame. 

        ```python
        import pandas as pd

        # All columns
        df_no_duplicates = df.drop_duplicates()

        # Specific columns
        df_no_duplicates_specific = df.drop_duplicates(subset = ['A', 'B'])

        # Specify which of the duplicates to keep
        df_first = df.drop_duplicates(keep = 'first')
        df_last = df.drop_duplicates(keep = 'last')
        ```

        - Using `set`: If the order of the rows are not important, each row can be converted into a tuple.

        ```python
        unique_rows = set(map(tuple, df.values()))
        df_no_dups_set = pd.DataFrame(list(unique_rows), columns = df.columns)
        ```

    - **Outlier Detection and Treatment**: Identify outliers using statistical methods or visualizations.  Decide whether to remove, transform, or leave outliers as is based on domain knowledge. 
        - Visual Inspection: Plot the data on a graph and inspect for points that deviate from the overall pattern.

        ```python
        import matplotlib.pyplot as plt
        import seaborn as sns

        # Box plot for visual inspection
        sns.boxplot(x = df['A'])
        plt.show()
        ```

        - Z-Score: This measures how many standard deviations a data point is from the mean. Values with high absolute z-scores are considered outliers.

        ```python
        from scipy import stats

        z_scores = stats.z_score(df['A'])
        threshold = 4 # Adjust according to preference
        outliers = df[abs(z_scores) > threshold]
        ```

        - Interquartile Range (IQR) Method: IQR is the range between the first and third quartiles. Values outside this range (with buffer) can be considered outliers.

        ```python
        iqr_q1 = df['A'].quantile(0.25)
        iqr_q3 = df['A'].quantile(0.75)
        iqr = iqr_q3 - iqr_q1

        lower_b = iqr_q1 - 1.5 * iqr
        upper_b = iqr_q3 + 1.5 * iqr

        outliers_iqr = df[(df['A'] < lower_b) | (df['A'] > upper_b)]
        ```

        - Clustering/Isolation Methods: There are ensemble methods that isolate outliers via recursively partitioning data, measure the local density deviation of a data point with respect to its neighbors, and group together closely packed points.

        ```python
        from sklearn.ensemble import IsolationForest
        from sklearn.neighbors import LocalOutlierFactor
        from sklearn.cluster import DBSCAN

        # Isolation Forest
        clf = IsolationForest(contamination = 0.05) # Adjust the contamination parameter
        outliers_if = clf.fit_predict(df[['A', 'B']])
        outliers_if_df = df[outliers_if == -1]

        # Local Outlier Factor (LOF)
        clf_lof = LocalOutlierFactor(contamination = 0.05) # Adjust the contamination parameter
        outliers_lof = clf_lof.fit_predict(df[['A', 'B']])
        outlier_lof_df = df[outliers_lof == -1]

        # DBSCAN (Density-Based Spatial Clustering of Applications with Noise)
        dbscan = DBSCAN(eps = 3, min_samples = 2) # Adjust parameters
        outliers_dbscan = df[dbscan.fit_predict(df[['A', 'B']]) == -1]
        ```

    - **Data Type Conversion**: Ensure data types are appropriate for analysis (e.g., converting text labels to numerical values). 
        - Using Constructor Functions: Python has built-in constructor functions for converting data types. You can use these to explicitly cast variables to different data types.

        ```python
        # Convert to integer
        integer_value = int("123")
        integer_value = int(123.45)

        # Convert to float
        float_value = float("123.45")
        float_value = float(123)

        # Convert to string
        str_value = str(123)
        ```

        - Pandas Data Type Conversion: You can use the `astype`, `map`, and `apply` methods to convert columns to different data types. Pandas also provides specific functions for converting to numeric or datetime types

        ```python
        # Convert to integer
        df['A'] = df['A'].astype(int)

        # Convert to float
        df['A'] = df['A'].astype(float)

        # Convert to string
        df['A'] = df['A'].astype(str)

        # Using map function
        df['A'] = df['A'].map(lambda x: int(x) if x.isdigit() else None)

        # Using apply function
        df['A'] = df['A'].apply(lambda x: str(x))

        # Convert to numeric
        df['A'] = pd.to_numeric(df['A'], errors = 'coerce')

        # Convert to datetime
        df['A'] = pd.to_datetime(df['A'])
        ```

        - Numpy Data Type Conversion: Numpy arrays also have an `astype` method for converting data types.

        ```python
        import numpy as np

        # Convert numpy array to integer
        int_array = np.array([1.1, 2.2, 3.3])
        int_array = np.array.astype(int)

        # Convert numpy array to float
        float_array = np.array([1, 2, 3])
        float_array = float_array.astype(float)
        ```

        - Literal Evaluation: Use `ast.literal_eval` if you need to convert a string representation of a literal to its corresponding value.

        ```python
        from ast import literal_eval

        string_list = "[1, 2, 3]"
        list_value = literal_eval(string_list)
        ```

{:style="counter-reset:none"}
1. Feature Engineering  
    - **Categorical Encoding**: Use appropriate encoding techniques for categorical features to convert them into numerical representations. Common methods include one-hot encoding, label encoding, or target encoding. Choose encoding methods that align with model interpretability requirements. 
        - One-Hot Encoding: Each category in a categorical column is re-represented as a binary column. 

        ```python
        from sklearn.preprocessing import OneHotEncoder

        # Using pandas get_dummies
        df_encoded = pd.get_dummies(df, columns = ['A', 'B', 'C'])

        # Using scikit-learn
        encoder = OneHotEncoder(sparse = False)
        df_encoded = pd.DataFrame(encoder.fit_transform(df[['A', 'B', 'C']]))
        ```

        - Label Encoding: This assigns a unique integer to each category, but still just keeping one column.

        ```python
        from sklearn.preprocessing import LabelEncoder
        
        le = LabelEncoder()
        df['A_encoded'] = le.fit_transform(df['A'])
        ```

        - Ordinal Encoding: This is suitable when there is an inherent order in the categories.

        ```python
        from sklearn.preprocessing import OrdinalEncoder

        oe = OrdinalEncoder(categories = ['low', 'medium', 'high'])
        df['A_encoded'] = oe.fit_transform(df['A'])
        ```

        - Hashing: This converts categories into a fixed number of hash buckets, thus reducing dimensionality.

        ```python
        from sklearn.feature_extraction import FeatureHasher

        hasher = FeatureHasher(n_features = 10, input_type = 'string')
        hashed_features = hasher.transform(df['A']).toarray()
        df_encoded = pd.DataFrame(hashed_features, columns = [f'hash_{i}' for i in range(10)])
        ```

    - **Feature Scaling and Normalisation**: Scaling features to a common range (e.g., [0, 1] or standardized with mean 0 and variance 1) can help models perform better and make their explanations more interpretable. Scaling ensures that all features contribute to the model on an equal footing. 
        - Min-Max Scaling: This scales the data between 0 and 1.

        ```python
        from sklearn.preprocessing import MinMaxScaler

        scaler = MinMaxScaler()
        X_scaled = scaler.fit_transform(X)
        ```

        - Standardization: This scales the data to have a mean of 0 and a standard deviation of 1.

        ```python
        from sklearn.preprocessing import StandardScaler
        scaler = StandardScaler()
        X_scaled = scaler.fit_transform(X)
        ```

        - Robust Scaling: This scales the data using the median and IQR, making it more robust to outliers.

        ```python
        from sklearn.preprocessing import RobustScaler

        scaler = RobustScaler()
        X_scaled = scaler.fit_transform(X)
        ```

        - Normalization: This normalizes each sample to have a unit norm.

        ```python
        from sklearn.preprocessing import Normalizer

        # L2 Regularization
        scaler = Normalizer(norm = 'l2')
        X_normalized = scaler.fit_transform(X)

        # L1 Regularization
        scaler = Normalizer(norm = 'l1')
        X_normalized = scaler.fit_transform(X)
        ```

        - Power Transformations: Apply these to make the data more Gaussian-like.

        ```python
        from sklearn.preprocessing import PowerTransformer

        scaler = PowerTransformer(method = 'yeo-johnson')
        X_transformed = scaler.fit_transform(X)
        ```

        - Log Transformation: Applying a logarithmic transformation to handle skewed distributions.

        ```python
        X_log_transforemd = np.log1p(X)
        ```

    - **Feature Selection**: Reduce the number of features by selecting the most important features. Techniques like feature importance from tree-based models or feature selection algorithms (e.g., Recursive Feature Elimination) can be useful. Feature selection can enhance model interpretability by focusing on the most relevant variables. 
        - Variance Threshold: This removes features with very low variance.

        ```python
        from sklearn.feature_selection import VarianceThreshold

        selector = VarianceThreshold(threshold = 0.1)
        X_selected = selector.fit_transform(X, y)
        ```

        - Univariate Feature Selection: Select features based on statistical tests like Chi-Squared, ANOVA, or mutual information.

        ```python
        from sklearn.feature_selection import SelectKBest, chi2, f_classif, mutual_info_classif

        selector = SelectKBest(score_func = chi2, k = 5) # or f_classif, mutual_info_classif
        X_selected = selector.fit_transform(X, y)
        ```

        - From initial models: These methods choose the most important features based on model performance.

        ```python
        from sklearn.feature_selection import RFE, SequentialFeatureSelector, RFA, SelectFromModel
        from sklearn.linear_model import LogisticRegression, Lasso
        from sklearn.ensemble import RandomForestClassifier

        # Recursive Feature Elimination (RFE) - recursively removes the least important features
        estimator = LogisticRegression()
        selector = RFE(estimator, n_features_to_select = 5)
        X_selected = selector.fit_transform(X, y)

        # L1 Regularization - encourages sparsity by applying penalties to the absolute values of the coefficients
        model = Lasso(alpha = 0.1)
        model.fit(X, y)
        selected_features = X.columns[model_coef! > 0.01] # Change threshold
        X_selected = X[selected_features]

        # Sequential Feature Selection - selects features sequentially based on model performance
        model = RandomForestClassifier()
        selector = SequentialFeatureSelector(model, n_features_to_select = 5, direction = 'forward')
        X_selected = selector.fit_transform(X, y)

        # Recursive Feature Addition (RFA) - Similar to RFE, but it adds features sequentially
        estimator = LogisticRegression()
        selector = RFA(estimator, n_features_to_select = 5)
        X_selected = selector.fit_transform(X, y)

        # SelectFromModel - Selects features based on the importance threshold
        model = RandomForestClassifier()
        selector = SelectFromModel(model, threshold = 'mean')
        X_selected = selector.fit_transform(X, y)
        ```

    - **Principal Component Analysis**: Use PCA for dimensionality reduction when dealing with high-dimensional data. PCA can help uncover the underlying structure in data while reducing complexity.  Visualize the first few principal components to understand which original features contribute most to them. 
        - Using scikit-learn: It provides a convenient implementation of PCA.

        ```python
        from sklearn.decomposition import PCA, IncrementalPCA, KernelPCA

        # Standardize the data
        scaler = StandardScaler()
        X_scaled = scaler.fit_transform(X)

        # Apply PCA
        pca = PCA(n_components = 4)
        X_pca = pca.fit_transform(X_scaled)

        # Incremental PCA to process data in chunks
        ipca = IncrementalPCA(n_components = 4)
        X_pca = ipca.fit_transform(X_scaled)

        # Kernel PCA for non-linear dimensionality reduction
        kpca = KernelPCA(n_components = 4, kernel = 'rbf')
        X_pca = kpca.fit_transform(X_scaled)
        ```

        - Using NumPy: We can leverage NumPy's linear algebra capabilities to perform PCA.

        ```python
        # Standardize the data
        mean = np.mean(X, axis = 0)
        std = np.std(X, axis = 0)
        X_scaled = (X - mean) / std

        # Calculate covariance matrix
        cov_matrix = np.cov(X_scaled, rowvar = False)

        # Calculate eigenvalues and eigenvectors
        eigenvalues, eigenvectors = np.linalg.eigh(cov_matrix)

        # Sort eigenvalues and corresponsidng eigenvectors
        idx = np.argsort(eigenvalues)[::-1]
        eigenvalues = eigenvalues[idx]
        eigenvectors = eigenvectors[:, idx]

        # Project data onto principal components
        X_pca = X_scaled.dot(eigenvectors[:, :4])
        ```

        - Using statsmodels: It also provides PCA implementation with additional statistical features.

        ```python
        import statsmodels.api as sm

        # Standardize the data
        scaler = StandardScaler()
        X_scaled = scaler.fit_transform(X)

        # Add a constant term for intercept
        X_scaled = sm.add_constant(X_scaled)

        # Fit PCA model
        pca = sm.PCA(X_scaled)
        pca_result = pca.fit()
        
        # Access principal components
        principal_components = pca_result.factors
        ```

        - Using TensorFlow: This can also be used for PCA, especially when handling large datasets.

        ```python
        import tensorflow as tf

        # Standardize the data
        scaler = StandardScaler()
        X_scaled = scaler.fit_transform(X)

        # Convert to TensorFlow tensors
        X_tensor = tf.constant(X_scaled, dtype = tf.float32)

        # Apply PCA using TensorFlow
        _, _, V = tf.linalg.svd(X_tensor)
        X_pca = tf.matmul(X_tensor, V[:, :4])
        ```

    - **XRAI Techniques**: Document all feature engineering steps and rationale behind these steps. Utilize SHAP values or partial dependence plots, to explain how individual features impact model predictions. Visualize feature importance to provide insights into which features are most influential in the model's decision-making process. 