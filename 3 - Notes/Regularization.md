Tags: [[__Machine_Learning]]

# Introduction
Regularization is a technique used during training machine learning models by minimalizing a loss function ([[Loss functions|link]]). If a model is not trained by loss minimization, regularization cannot be applied.

It improves generalization of models (prevent overfitting) by making model parameters smaller and more similar to each other.

Parameters are made smaller by adding a penalty function to the loss:
$$
\text{Regularized loss} = \text{Original loss} + \lambda \cdot \text{Penalty}
$$
where:
- $\lambda$ - controls the strength of regularization
- Penalty depends on model parameters - bigger parameters = bigger penalty

Because bigger parameters make the entire loss bigger, minimizing loss causes parameters to be small as well.
# Why it helps
Bigger parameters cause that features corresponding to those parameters have bigger impact on the prediction.

For example, in case of the linear regression ([[Linear Regression|link]]), model makes predictions using this formula:
$$
\hat{y} = w_0 + w_1 * x_1 + ... + w_n * x_n = Xw
$$
Each parameter $w_i$ determines how strongly its corresponding feature $x_i$ influences the prediction. Bigger value of a parameter, causes the model to be more sensitive to changes in value of the corresponding feature.

That's why regularization, by making parameters smaller and more similar to each other, prevents a single feature having too big impact on the prediction.
# Feature selection
Some regularizations, e.g. L1 regularization ([[L1 Regularization (Lasso)|link]]), tend to reduce parameter values to zero.

When we reduce parameter to zero, that means that features corresponding to that parameter doesn't make any impact on the prediction.

That's why reducing parameters to zero is called 'feature selection', it selects features which will have an impact on the prediction.

Models which have a lot of parameters equal to zero are called **sparse models**, so they rely only on a subset of all features.
# Examples of regularization
Below are common examples of regularization with links to materials from which we can learn more about them:
- L2 Regularization (Ridge) - [[L2 Regularization (Ridge)|link]]
- L1 Regularization (Lasso) - [[L1 Regularization (Lasso)|link]]
- Elastic Net Regularization - [[Elastic Net Regularization|link]]
# Relation to MAP Estimation
Regularization is also related to the MAP Estimation ([[Relation between MAP and minimizing loss with regularization|link]]). Using MAP Estimation is equivalent to minimizing a loss function with a regularization.

Seeing that relation helps to understand why regularization can be interpreted as a measure of how 'surprised' we are by observing model parameters $\theta$ obtained from training the model, according to our belief about parameters $\theta$ we assumed before training the model.

#MachineLearning 