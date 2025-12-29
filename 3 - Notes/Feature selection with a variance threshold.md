Tags: [[__Machine_Learning]]

# Introduction
Feature selection with a variance threshold is a technique for a dimensionality reduction ([[Dimensionality reduction|link]]) which reduces number of features ([[Dataset of observations of random variables X, Y - Variables per sample, feature and target variable|link]]) by eliminating those with the lowest variance.
# How it works
We calculate the estimated variance for each feature $X_i$ :
$$
\large
\hat{\sigma}^2 = \frac{1}{n-1} \sum_{i=1}^n (x_i - \bar{x})^2, \quad
\bar{x} = \frac{1}{n} \sum_{i=1}^n x_i
$$
And we choose features which has that variance higher than a chosen threshold.
# Interpretation
When a feature $X$ has a higher variance, that means that there is more different values of that feature across all the data samples in a dataset.

It might help a model to detect the relation between that feature $X$ and the target variable $Y$ because model sees how value of $Y$ differs across different values of $X$.

If we have the same feature value in each data sample in a training dataset ([[Train - test split of a dataset|link]]), then models learns only how the target variable $Y$ looks like for this feature value. After training, when that model sees a different value of that feature, it would not know how $Y$ will behave.

Note, that higher variance of a feature $X$ doesn't always mean that it is more useful for predicting the target variable $Y$. Sometimes, $Y$ depends strongly on features with a small variance, for example on some rare events.
# Cons
- It doesn't consider the relationship between a given feature $X$ and the target variable $Y$
- Sensitive to feature scaling - Large-valued features have large variance
- 

#MachineLearning 