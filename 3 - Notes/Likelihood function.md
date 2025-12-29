Tags: [[__Machine_Learning]]

# Notation and shorthands
This document uses notation and shorthands which are described here - [[Mathematical general notations and shorthands|link]].
# Introduction
A likelihood function is a function used to measure how well a statistical model explains given dataset consisting of observations of random variables.

It describes how probable are given observations of random variables for different parameters of a their probability distribution function ([[Probability distribution - Introduction|link]]) which is defined by a statistical model.

Or we can also say that it describes what is a probability that given set of random variables returns given numbers.

For the precise interpretation, refer to the section 'Interpretation' further in this document.

It is used for example in the Maximum Likelihood Estimation (MLE) method ([[Maximum Likelihood Estimation (MLE)|link]]) which finds the best parameters for statistical models for classification and regression by choosing such a parameters, that maximizes the likelihood function.

Sometimes, in order to maximize the likelihood function, we minimize the negative log-likelihood function instead what is equivalent and simpler to do.
# Likelihood function formula
Likelihood function formula depends on the considered type of probability.
## Joint probability
Let's assume, we have a dataset $D = \{x_i\}_{i=1}^n$ with observations of random variables $X_i$ as described here - [[Dataset of observations of random variable X - Variables per sample and variable]].

$\Large p_{X_{1:n}}(x_{1:n}; \theta)$ is a joint probability distribution function of $X$ with a set of parameters given by the vector $\theta$.

The likelihood function is a function of the parameter $\theta$ :
$$
\Large
L(\theta) = p_{X_{1:n}}(x_{1:n}; \theta)
$$
If random variables are independent ([[Independency of random variables|link]]), then:
$$
\large
L(\theta) = \prod_{i=1}^n p_{X_i}(x_i; \theta)
$$
where $\large p_{X_i}(x_i; \theta)$ is a marginal probability distribution function ([[Marginal probability distribution function|link]]) for the variable $X_i$.
## Conditional probability
Let's assume, that we have a dataset $D = \{ (x_i, y_i) \}_{i=1}^n$ with observations of random variables $X_i, Y_i$ like described here - [[Dataset of observations of random variables X, Y - Variables per sample, feature and target variable]].

$\Large p_{Y_{1:n} \mid X_{1:n}}(y_{1:n} \mid x_{1:n}; \theta)$ is a joint conditional probability distribution function ([[Conditional probability distribution (density, mass) function|link]]) of $Y$ given $X$ with a set of parameters given by the vector $\theta$.

Then conditional likelihood function is a function of the parameter $\theta$ :
$$
\Large
L(\theta) = p_{Y_{1:n} \mid X_{1:n}}(y_{1:n} \mid x_{1:n}; \theta)
$$
If $Y_i$ are conditionally independent given $\large X_{1:n}$ and $Y_i$ is depends only on the corresponding $X_i$, then:
$$
\large
L(\theta) = \prod_{i=1}^n p_{Y_i \mid X_i}(y_i \mid x_i; \theta)
$$
where $\large p_{Y_i \mid X_i}(y_i \mid x_i; \theta)$ is a marginal conditional probability distribution function ([[Marginal conditional probability distribution function|link]]) for the variable $Y_i$ given $X_i$.
# Negative log-likelihood function formula
Negative log-likelihood function is given by the formula:
$$
\large
- l(\theta) = - \sum_{i=1}^n \log(p_{X_i}(x_i; \theta))
$$
# Interpretation
When our dataset $D$ consists of observations of discrete random variables, we can literally say that likelihood function describes probability of observing such a dataset because:
$$
\Large
L(\theta) = p_{X_{1:n}}(x_{1:n}; \theta) = P_\theta(\bigwedge_{i=1}^n X_i = x_i) = P(D)
$$

That equation is described here - [[Probability distribution function - Discrete random variables|link]] in the section about 'Equation for probability $X_i = x_i$'.

In case of continuous random variables ([[Probability distribution function - Continuous random variables|link]]) probability of observing our exact dataset is zero:
$$
P_\theta(\bigwedge_{i=1}^n X_i = x_i) = 0
$$
but density at that point $\Large p_{X_{1:n}}(x_{1:n})$ also gives us some idea about probability of observing this dataset.

If $\Large p_{X_{1:n}}$ has high value at the $\large x_{1:n}$ point, then it has also similar, high values in a close surrounding of $\large x_{1:n}$ (because it is a continuous function):
$$
A = \prod_{i=1}^n A_i, \quad A_i = [x_i - \epsilon, x_i + \epsilon]
$$
where $\epsilon$ is small, close to 0.

So probability that our observed dataset has values in that close surrounding (similar to the observed dataset $D$) is also high:
$$
\Large
P_\theta(\bigwedge_{i=1}^n X_i \in A_i) = \int_{A_{1:n}} 
p_{X_{1:n}}(x_{1:n}) dx_{1:n}
$$

#MachineLearning 