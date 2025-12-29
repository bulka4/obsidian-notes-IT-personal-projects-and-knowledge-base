Tags: [[__Machine_Learning]]

# Notation and shorthands
This document uses notation and shorthands which are described here - [[Mathematical general notations and shorthands|link]].
# Introduction
Maximum Likelihood Estimation (MLE) is a method of training statistical models (finding the best parameters) for classification and regression models.

Parameters are chosen in such a way, as to maximize the likelihood function ([[Likelihood function|link]]) which value depends on the model we train. 

By doing that, we maximize the probability of observing given realizations of random variables, which is calculated using our model.

Maximizing the likelihood function is often done by minimizing the negative log-likelihood function using gradient descent algorithm ([[Gradient Descent - ML|link]]), what is equivalent and easier to do.
# Using MLE for training ML models
Let's assume, that we have a dataset $D = \{ (x_i, y_i) \}_{i=1}^n$ with observations of random variables $X_i, Y_i$ like described here - [[Dataset of observations of random variables X, Y - Variables per sample, feature and target variable]].

In MLE we additionally assume that random variables $Y_i$ are conditionally independent given $\large X_{1:n}$ ([[Independency of random variables|link]]) and $Y_i$ is dependent only on the corresponding $X_i$.

That allows us to write the formula for the likelihood as:
$$
\Large
L(\theta) = p_{Y_{1:n} \mid X_{1:n}}(y_{1:n} \mid x_{1:n}; \theta) = 
\prod_{i=1}^n p_{Y_i \mid X_i}(y_i \mid x_i ; \theta)
$$
and MLE finds parameters which maximizes the likelihood function:
$$
\hat{\theta}_{MLE} = \text{arg} \max_{\theta}L(\theta)
$$
To use MLE for training machine learning models, we define the probability distribution function $\large p_{Y_i \mid X_i}(y \mid x ; \theta)$ using the model we want to train, so we have:
$$
\large 
p_{Y_i \mid X_i}(y \mid x ; \theta) = g(f_\theta(x))
$$
for some function $g$, where $f_\theta$ is our model.

So that means that:
- The model is used to calculate probabilities of observing realizations of random variables (observing that random variables return specific values) 
- We find such parameters $\theta$ for which probability of observing realizations from a given dataset, according to the model, is the highest.
## MLE for classification
Using MLE for training models for classification gives us formula for the Cross-Entropy loss function. More information about it can be found here - [[Cross-Entropy]].
## MLE for regression
Using MLE for training models for regression gives us formula for the Mean Squared Error (MSE) loss function. More information about it can be found here - [[MSE (Mean Squared Error)]].
# Minimizing the negative log-likelihood function
Sometimes the product in the formula for $L(\theta)$ can be very small and performing calculations for finding the maximum can be difficult. 

That's why in practice we often maximize the likelihood function by minimizing the **negative log-likelihood function** (i.e. Cross-Entropy loss function - [[Cross-Entropy|link]]) using gradient descent algorithm:
$$
\Large
- l(\theta) = - \sum_{i=1}^n \log(p_{Y_i \mid X_i}(y_i \mid x_i ; \theta))
$$
That works because:
- Maximizing the likelihood function is equivalent to maximizing the log-likelihood function
- And that is equivalent to minimizing the negative log-likelihood function

# Related topics
- [[Likelihood function]]
- [[Dataset of observations of random variables X, Y - Variables per sample, feature and target variable]]
- [[Random variable]]
- [[Gradient Descent - ML]]
- [[Logistic Regression]]
- [[Cross-Entropy]
- [[Loss functions]]
- 
#MachineLearning 