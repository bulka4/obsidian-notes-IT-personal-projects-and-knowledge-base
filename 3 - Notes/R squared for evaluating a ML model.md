Tags: [[__Machine_Learning]]

# Introduction
R squared ($R^2$, Coefficient of Determination) is a metric is used for evaluating regression models. It indicates how well model explains the variance in the target variable we are trying to predict. It is a value between 0 and 1.

Formula:
$$
R^2 = 1 - \frac{\sum_{i=1}^n(y_i - \hat{y_i})^2}{\sum_{i=1}^n(y_i - \bar{y})^2}
$$
Where:
- $\bar{y}$ - mean of true values
- $y_i$ - true value
- $\hat{y_i}$ - predicted value

If $R^2$ equals 1, it means that model fits perfectly.
If $R^2$ equals 0, it means that model predicts no better than a mean (always predicting a mean).

#MachineLearning 