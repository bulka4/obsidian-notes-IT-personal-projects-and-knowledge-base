Tags: [[__Machine_Learning]]

# Introduction
Training machine learning models is often done by minimalizing a loss function.

Loss function represents an error made by a model when making predictions which we want to minimalize. We can use for example the gradient descent ([[Gradient Descent - ML|link]]) algorithm for that purpose.
# How loss functions are derived
Loss functions are chosen in such a way, that minimalizing it is equivalent to one of the options:
- Maximizing the probability of observing given realizations of random variables (Maximum Likelihood Estimation (MLE) (more information here - [[Maximum Likelihood Estimation (MLE)|link]]))
- Minimizing a divergence or distance between probability distributions (more information here - [[Minimizing divergence between probability distributions|link]]) — e.g., Kullback–Leibler divergence, cross-entropy, or other objectives derived from Bayesian or information-theoretic principles;
- Minimizing an expected risk (decision-theoretic loss) — where the loss represents the cost of prediction errors under a specific utility or margin-based criterion.
- Minimizing distance if a feature space - Encourages relative relationships (similar/dissimilar) rather than exact labels. Can be interpreted as minimizing an expected “distance-based risk” rather than standard MSE or CE. For example Triplet loss, contrastive loss.
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
# Related topics
1. Gradient descent - [[Gradient Descent - ML|link]]

#MachineLearning 