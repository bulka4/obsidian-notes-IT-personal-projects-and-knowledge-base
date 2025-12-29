Tags: [[__Machine_Learning]]

# Notation and shorthands
This document uses notation and shorthands which are described here - [[Mathematical general notations and shorthands|link]].
# Introduction
We can express the empirical approximation of Cross-Entropy using a likelihood function as described here - [[Empirical approximation of Cross-Entropy]].

Minimizing Cross-Entropy is equivalent to maximizing value of a likelihood function, thus that is equivalent to the Maximum Likelihood Estimation ([[Maximum Likelihood Estimation (MLE)|link]]).
# Assumptions
Let's assume, that:
- We have a dataset $D = \{ (x_i, y_i) \}_{i=1}^n$ with observations of random variables $X_i, Y_i$ like described here - [[Dataset of observations of random variables X, Y - Variables per sample, feature and target variable|link]].
- Pairs $(X_i, Y_i)$ are i.i.d. copies of $(X, Y)$ and $Y_i$ depends only on the corresponding $X_i$ (as described here - [[Independent and identically distributed (i.i.d.) pairs of random variables|link]])
- $y_i, x_i$ are observations of random variables $X_i, Y_i$ for every $i$ ([[Observations - realizations of random variables|link]])
# Cross-Entropy empirical approximation
The conditional formula for Cross-Entropy with a non-fixed condition ([[Cross-Entropy#Non-fixed condition|link]]) is:
$$
H(P, Q) = \mathbb{E}_{P(X, Y)}(-\log(q_\theta(Y \mid X)))
$$
where $\large q_\theta(y \mid x) = \frac{dQ}{d\mu}(y \mid x) = p_{Y \mid X}(y \mid x ; \theta)$ is a conditional probability distribution function.

It can be empirically approximated ([[Empirical approximation of Cross-Entropy|link]]) using the law of large numbers and the assumption that pairs $(X_i, Y_i)$ are i.i.d. copies of $(X, Y)$:
$$
-\frac{1}{n} \sum_{i=1}^n \log(p_{Y \mid X}(y_i \mid x_i)) \approx \mathbb{E}_{P(X, Y)}(-\log(p_{Y \mid X}(Y \mid X)))
$$
# Likelihood
The likelihood function formula is:
$$
\Large
L(\theta) = p_{Y_{1:n} \mid X_{1:n}}(y_{1:n} \mid x_{1:n}; \theta)
$$
And since random variables are i.i.d., then that equals to:
$$
\large
L(\theta) = \prod_{i=1}^n p_{Y_i \mid X_i}(y_i \mid x_i; \theta)
$$
and negative log-likelihood is:
$$
\large
- l(\theta) = -\log(L(\theta)) = - \sum_{i=1}^n \log(p_{Y_i \mid X_i}(y_i \mid x_i; \theta))
$$
Since $X_i, Y_i$ are identically distributed as $X, Y$, then $\large p_{Y \mid X} = p_{Y_i \mid X_i}$.
# Cross-Entropy and Likelihood relation
So we have:
$$
H(P, Q) = \mathbb{E}_{P(X, Y)}(-\log(p_{Y \mid X}(Y \mid X))) \approx 
- \frac{1}{n} \sum_{i=1}^n \log(p_{Y \mid X}(y_i \mid x_i)) = 
- \frac{1}{n} \log(L(\theta))
$$
# Maximizing likelihood
Minimizing this Cross-Entropy formula is equivalent to maximizing value of the likelihood function $L(\theta)$, that's why we say that it is equivalent to the MLE method.
# Training models
For training statistical models, we assume that:
- $P$ is the true probability distribution ([[Probability distribution|link]]) of $Y \mid X$ 
- $q_\theta$ is  defined by a statistical model

It is described here - [[Cross-Entropy for classification]].

#MachineLearning 