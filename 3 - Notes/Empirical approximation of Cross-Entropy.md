Tags: [[__Machine_Learning]]

# Notation and shorthands
This document uses notation and shorthands which are described here - [[Mathematical general notations and shorthands|link]].
# Introduction
Cross-Entropy ([[Cross-Entropy|link]]) can be used to train statistical models as described here - [[Cross-Entropy for classification]].

We can't calculate the Cross-Entropy precisely as it is a theoretical value. It uses the true probability distribution $P$ of random variables $X, Y$ which is unknown.

So in order to use it for training models, we need to calculate its empirically approximated value.

That empirical approximation uses the likelihood function ([[Likelihood function|link]]) formula, so that links Cross-Entropy to the Maximum Likelihood Estimation as described here - [[Relation of Cross-Entropy to the Maximum Likelihood Estimation|link]].

Also that gives us another interpretation of Cross-Entropy which is the same as for likelihood function - that it describes probability of observing given realizations of random variables calculated using the model we train.
# Empirical approximation of Cross-Entropy
Empirical approximation of Cross-Entropy can be calculated using the law of large numbers.

Let's assume, that:
- We have a dataset $D = \{ (x_i, y_i) \}_{i=1}^n$ with observations of random variables $X_i, Y_i$ like described here - [[Dataset of observations of random variables X, Y - Variables per sample, feature and target variable|link]].
- Pairs $(X_i, Y_i)$ are i.i.d. copies of $(X, Y)$ and $Y_i$ depends only on the corresponding $X_i$ (as described here - [[Independent and identically distributed (i.i.d.) pairs of random variables|link]])
- $y_i, x_i$ are observations of random variables $X_i, Y_i$ for every $i$ ([[Observations - realizations of random variables|link]])
- $P$ - Joint probability distribution of $(X, Y)$ 
- $Q$ - Conditional probability distribution of $Y \mid X$ 
- $\large q = \frac{dQ}{d\mu}$ is a probability distribution function
## Conditional probability with a non-fixed condition
In case of a conditional probability with a non-fixed condition, Cross-Entropy formula is:
$$
\mathbb{E}_{P(X, Y)}(-\log(q(Y \mid X)))
$$
By the law of large numbers, because pairs $(X_i, Y_i)$ are i.i.d. copies of $(X, Y)$, we have:
$$
\large
-\frac{1}{n} \sum_{i=1}^n \log(q(y_i \mid x_i)) \xrightarrow{n \to \infty} 
\mathbb{E}_{P(X, Y)}(-\log(q(Y \mid X)))
$$
So the average:
$$
-\frac{1}{n} \sum_{i=1}^n \log(q(y_i \mid x_i)) \approx \mathbb{E}_{P(X, Y)}(-\log(q(Y \mid X)))
$$
Can be used as an empirical approximation of Cross-Entropy.
## Conditional probability with a fixed condition
In case of Conditional probability with a non-fixed condition, Cross-Entropy formula is:
$$
\large
\mathbb{E}_{P(Y \mid X = x)}(-\log(q(Y \mid x)))
$$

where $X = x$ is a fixed condition.

By the law of large numbers, because pairs $(X_i, Y_i)$ are i.i.d. copies of $(X, Y)$, we have:
$$
\large
-\frac{1}{n} \sum_{i=1}^n \log(q(y_i \mid x_i)) \xrightarrow{n \to \infty} 
\mathbb{E}_{P(Y \mid X = x)}(-\log(q(Y \mid x))) = H(P, Q)
$$
So the average:
$$
-\frac{1}{n} \sum_{i=1}^n \log(q(y_i \mid x_i)) \approx \mathbb{E}_{P(Y \mid X = x)}(-\log(q(Y \mid x))) = H(P, Q)
$$
can be used as an empirical approximation of Cross-Entropy.
# Likelihood function
Approximated value of Cross-Entropy is the same formula as for the negative log-likelihood, if we use a parametric function $q_\theta = q$ :
$$
\large
\begin{align}
 & - l(\theta) = -\log(L(\theta)) = 
- \sum_{i=1}^n \log(p_{Y_i \mid X_i} (y_i \mid x_i; \theta)) = 
- \frac{1}{n} \sum_{i=1}^n \log(q_\theta(y_i \mid x_i))
\approx \\
 & \quad \approx \mathbb{E}_{P(Y \mid X = x)}(-\log(q_\theta(Y \mid x))) = H(P, Q)
\end{align}
$$

#MachineLearning 