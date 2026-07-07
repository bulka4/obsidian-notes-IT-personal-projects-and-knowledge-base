Tags: [[__Machine_Learning]]
#MachineLearning 

# Introduction
Training machine learning models is often done by minimalizing a loss function.

Loss function represents an error made by a model when making predictions which we want to minimalize. We can use for example the gradient descent ([[Gradient Descent - ML|link]]) algorithm for that purpose.
# How loss functions are derived
[[How loss functions are derived]].
# Regularization
Additionally, when training a model, we can use **regularization** in the loss function as described here -  [[Regularization]].

It helps with obtaining model parameters smaller and more similar to each other after training, what improves generalization of a model (prevents overfitting).

Also it helps with a feature selection, that is selecting those features from the dataset, which has a significant impact on the target variable we want to predict, and making a model to rely on those features while ignoring others.

Regularization is also related to the MAP Estimation ([[Relation between MAP and minimizing loss with regularization|link]]). Using MAP Estimation is equivalent to minimizing a loss function with a regularization.
# Different types of loss functions
There are different loss functions for regression and for classification.

For regression, the most common ones include:
- MSE (Mean Squared Error) - More information [[MSE (Mean Squared Error)|here]]

For classification, the most common ones include:
- Cross-Entropy (for both multi-class and binary classification) - More information [[Cross-Entropy|here]]
# Minimizing a loss function
In order to minimize a loss function, we use usually gradient-based optimization algorithms ([[ML - Gradient-based optimization|link]]), like gradient descent ([[Gradient Descent - ML|link]]) or Adam ([[Adam optimizer|link]]).
# Related topics
1. Gradient descent - [[Gradient Descent - ML|link]]

#MachineLearning 