Tags: [[__Machine_Learning]]

# Notation and shorthands
This document uses notation and shorthands which are described here - [[Mathematical general notations and shorthands|link]].
# Introduction
MSE (Mean Squared Error) is a loss function ([[Loss functions|link]]) for regression models.

MSE formula is derived from using Maximum Likelihood Estimation (MLE) for continuous random variables. Minimalizing the MSE is equivalent to maximizing the likelihood function.

We use a model to define the values $\large p_{Y_i \mid X_i}(y_i \mid x_i; \theta)$ needed for calculating a likelihood by assuming the distribution:
$$
Y_i \mid X_i \sim \mathcal{N} (f_\theta(X_i), \sigma^2)
$$
where $f_\theta$ is our model.
# MSE formula
MSE is calculated using the formula:
$$
MSE = \frac{1}{m} \sum_{i=1}^{m} (y_i - \hat{y}_i)^2
$$
where:
- $m$ is number of samples
- $y_i$ is a true value
- $\hat{y_i}$ is a predicted value
# MSE relation to MLE (Maximum Likelihood Estimation)
MSE formula is derived from using Maximum Likelihood Estimation (MLE) for continuous random variables. Minimalizing the MSE is equivalent to maximizing the likelihood function.

To see how exactly they are related, refer to the document here - [[MSE relation to MLE (Maximum Likelihood Estimation)]].
# Relation to Cross-Entropy
MSE is related to MLE and MLE is further related to Cross-Entropy as described here - [[Relation of Cross-Entropy to the Maximum Likelihood Estimation]].

So MSE is related to Cross-Entropy as well. Minimizing MSE minimizes Cross-Entropy.

#MachineLearning 