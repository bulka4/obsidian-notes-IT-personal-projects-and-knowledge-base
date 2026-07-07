Tags: [[__Machine_Learning]]
#MachineLearning 

# Introduction
We always assume what probability distribution $Y|X$ model represents / defines. We assume, that model outputs parameters of a specific probability distribution.

This is used to derive a loss function ([[How loss functions are derived|link]]).
# Example
For regression, we can for example assume that model output is $\mu(x)$, where:
$$
Y | X = x \sim \mathcal{N}( \mu(x) , \sigma^2)
$$
so this is a mean (the most likely value) of $Y$ given $X$.

For a binary classification, we can assume that model outputs $p(x)$, where:
$$
Y | X = x \sim \text{Bernoulli}(p(x))
$$

For a multi-class classification, we can assume that model outputs $p_1(x), ..., p_n(x)$, where:
$$
\begin{align}
& Y | X = x \sim \text{Categorical}(p_1(x), ..., p_n(x))
\\ & \sum p_i = 1
\end{align}
$$
