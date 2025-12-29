Tags: [[__Machine_Learning]]

# Introduction
Below are described methods we can use when we have missing data (values for some features in a dataset are empty).
## Understand the Missingness

First, check why the data is missing:
1. MCAR (Missing Completely at Random)
    - Missingness has no pattern; it's purely random.
    - E.g., survey accidentally skipped a question.
2. MAR (Missing at Random)
    - Missingness depends on observed data.
    - E.g., income data missing more often for certain age groups.
3. MNAR (Missing Not at Random)
    - Missingness depends on unobserved data itself.
    - E.g., high earners tend to skip income questions.

Why this matters: The strategy you choose can introduce bias if missingness is not random.
## Basic Approaches
### A. Remove Missing Data
- Drop rows (`listwise deletion`) or columns with missing values.
- Works when:
    - Very few missing points
    - Dropping them won’t bias the data
- Limitation: can waste valuable data if missingness is high.
### B. Impute Missing Values
#### Simple Imputation
- Fill with:
    - Mean, median, or mode
    - Constant (e.g., 0 or “Unknown”)
- Pros: simple, fast
- Cons: can reduce variance, ignore correlations
#### Forward/Backward Fill
- For time series:
    - Forward fill: use last known value
    - Backward fill: use next known value
- Pros: simple, preserves trend
- Cons: may propagate errors
#### Interpolation
- Fill in missing values assuming some relationship between the surrounding points.
- Linear, spline, or polynomial interpolation
- Good for numerical time series
#### K-Nearest Neighbors (KNN) Imputation
- Impute based on similar samples
- Pros: captures local structure
- Cons: computationally expensive for large datasets
#### Multivariate Imputation / MICE
- Multiple Imputation by Chained Equations
- Models each feature as a function of others
- Pros: statistically sound, handles MAR
- Cons: more complex, slower
### C. Model-Based Imputation
- Use machine learning to predict missing values:
    - Random Forest, XGBoost, or Neural Networks
- Can capture nonlinear patterns between features
### D. Special Values / Indicators
- Sometimes, you create a “missing” category for categorical features.
- Or add a binary indicator for missingness to let the model learn the pattern.

#MachineLearning 