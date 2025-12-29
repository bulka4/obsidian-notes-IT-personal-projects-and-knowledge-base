Tags: [[__Machine_Learning]]

# Notation and shorthands
This document uses notation and shorthands which are described here - [[Mathematical general notations and shorthands|link]].
# Introduction
Cross-Entropy ([[Cross-Entropy|link]]) can be used as a loss function ([[Loss functions|link]]) for classification models ([[Classification models|link]]), for both binary and multi-class classifications.

Its formula depends on whether we use it for a multi-class or a binary classification. Those formulas are written in the sections below corresponding to each classification type.
# Overview of training using Cross-Entropy
## Cross-Entropy formula and assumptions
Cross-Entropy general formula is:
$$
H(P, Q) = -\mathbb{E}_{P(X, Y)}(\log(\frac{dQ}{d\mu}(Y \mid X)))
$$
where:
- $\large q = \frac{dQ}{d\mu}$ - Probability distribution function of $Y \mid X$ 

Let's assume, that:
- We have a dataset $D = \{ (x_i, y_i) \}_{i=1}^n$ with observations of random variables $X_i, Y_i$ like described here - [[Dataset of observations of random variables X, Y - Variables per sample, feature and target variable|link]].
- Pairs $(X_i, Y_i)$ are i.i.d. copies of $(X, Y)$ and $Y_i$ depends only on the corresponding $X_i$ (as described here - [[Independent and identically distributed (i.i.d.) pairs of random variables|link]])
- $y_i, x_i$ are observations of random variables $X_i, Y_i$ for every $i$ ([[Observations - realizations of random variables|link]])
- $P$ - True probability distribution of $(X, Y)$ 
- We have a model $f_\theta$ ([[What is a Machine Learning model|link]]) we want to train, which is a parametric function with parameters $\theta$ 
- $q = q_\theta$ is a parametric function with parameters $\theta$ and it is defined by the model $f_\theta$ we train, so there exists a function $g$ such that $q_\theta = g(f_\theta)$.
## How to use Cross-Entropy
We train a model by finding such parameters $\theta$, which minimizes Cross-Entropy. Why we minimize it, is explained in the next section.

We can't calculate the Cross-Entropy precisely as it is a theoretical value. It uses the true probability distribution $P$ of random variables $X, Y$ which is unknown.

We can only approximate it, as shown here - [[Empirical approximation of Cross-Entropy]], using observations $x_i, y_i$ from random variables $X_i, Y_i$ which copies of the true random variables $X, Y$.

Approximated formula is:
$$
\large
CE = - \frac{1}{n} l(\theta) = -\frac{1}{n} \log(L(\theta)) = - \frac{1}{n} \sum_{i=1}^n \log(p_{Y_i \mid X_i}(y_i \mid x_i; \theta))
$$
Which uses the likelihood function $L(\theta)$ ([[Likelihood function|link]]).

To get values $\large p_{Y_i \mid X_i}(y_i \mid x_i; \theta)$ needed for calculating it, we assume that those values are model's output:
$$
\large
f_\theta(x_i) = \{P(Y_i = y_j \mid X_i = x_i; \theta)\}_{j=1}^K = \{ p_{Y_i \mid X_i}(y_j \mid x_i; \theta)\}_{j=1}^K
$$
where $f_\theta$ is our model.
## Why to minimize Cross-Entropy
We chose such a parameters $\theta$ for the model $f_\theta$, for which Cross-Entropy is as low as possible because:
- Low values of Cross-Entropy indicates that when the distribution $P$ assigns a high probability to some event, then modeled distribution $Q$ also assigns high probability as described here - [[Cross-Entropy#Interpretation|link]] in the 'Interpretation' section.
- Also, as explained here:
	- [[Relation of Cross-Entropy to the Maximum Likelihood Estimation]]
	- [[Likelihood function]]
  minimizing Cross-Entropy is equivalent to maximizing the likelihood function, so we are maximizing the probability of observing given realizations of random variables, which we use for training the model.
- As explained here - [[Relation between KL Divergence and Cross-Entropy and Entropy]], lower value of Cross-Entropy implies lower value of KL Divergence, which, as described here - [[KL Divergence]], in the 'Interpretation' section, indicates that when distribution $P$ assigns a high probability to some event, then the difference between probabilities assigned to that event by the modeled distribution $Q$ and $P$ is small.
# Assumptions
We need the following assumptions to use Cross-Entropy for training models:
- We have a dataset $D = \{ (x_i, y_i) \}_{i=1}^n$ with observations of random variables $X_i, Y_i$ like described here - [[Dataset of observations of random variables X, Y - Variables per sample, feature and target variable|link]].
- Pairs $(X_i, Y_i)$ are i.i.d. copies of $(X, Y)$ and $Y_i$ depends only on the corresponding $X_i$ (as described here - [[Independent and identically distributed (i.i.d.) pairs of random variables|link]])
- $y_i, x_i$ are observations of random variables $X_i, Y_i$ for every $i$ ([[Observations - realizations of random variables|link]])
- Machine learning model is a parametric function $f_\theta:\ \mathcal{X} \rightarrow \mathcal{Y}$ as described here - [[What is a Machine Learning model|link]].
- Model output represents class probabilities: $f_\theta(x_i) = \{P(Y_i = y_j \mid X_i = x_i; \theta)\}_{j=1}^K$ as described here - [[Machine Learning model output as probabilities for classes|link]].

Thanks to the independency of random variables, the likelihood is a product of probabilities: 
$$
\Large
L(\theta) = p_{Y_{1:n} \mid X_{1:n}}(y_{1:n} \mid x_{1:n}; \theta)
= \prod_{i=1}^n p_{Y_i \mid X_i}(y_i \mid x_i; \theta)
$$
# Cross-Entropy additional requirements
Except for satisfying conditions from assumptions, below requirements needs to be satisfied as well to use Cross-Entropy for training models:
- Model is differentiable with respect to model parameters - So we can compute gradients for optimization (minimalizing the negative log-likelihood function) using e.g. gradient descent
# Cross-Entropy general formula using likelihood
As described here - [[Relation of Cross-Entropy to the Maximum Likelihood Estimation]], the empirical, approximated formula for Cross-Entropy ([[Cross-Entropy|link]]) is equivalent to the negative log-likelihood function ([[Likelihood function|link]]) with optionally added $\frac{1}{n}$ fraction to represent the average loss per sample.

So, for given observations $x_i,\ y_i$, Cross-Entropy equals:
$$
\large
CE = - \frac{1}{n} l(\theta) = -\frac{1}{n} \log(L(\theta)) = - \frac{1}{n} \sum_{i=1}^n \log(p_{Y_i \mid X_i}(y_i \mid x_i; \theta))
$$
So minimizing this Cross-Entropy formula is equivalent to maximizing value of the likelihood function $L(\theta)$, that's why we say that it is equivalent to the Maximum Likelihood Estimation method.
# Using model to calculate Cross-Entropy
To calculate Cross-Entropy, we need values $\large p_{Y_i \mid X_i}(y_i \mid x_i; \theta)$. We can get them from our model.

From assumptions, model outputs are probabilities for each class:
$$
f_\theta(x_i) = \{P(Y_i = y_j \mid X_i = x_i; \theta)\}_{j=1}^K
$$
and for discrete variables $Y_i$ we have:
$$
\large p_{Y_i \mid X_i}(y_i \mid x_i; \theta) = P(Y_i = y_i \mid X_i = x_i ; \theta)
$$
as described here - [[Conditional probability distribution function - Discrete random variables#Equation for probability $Y_i = y_i$|link]]. 

So to calculate Cross-Entropy, we can pick from the model's output needed value 
$$
P(Y_i = y_i \mid X_i = x_i ; \theta)
$$
which is the $i$-th element from the model's output $f_\theta(x_i)$ ($j = i$).

Alternatively, we can use one of the formulas described in sections below which calculates Cross-Entropy using all the probabilities
$$
P(Y_i = y_j \mid X_i = x_i ; \theta),\ j = 1, \ldots, K
$$
from the model's output.
## Multi-class classification
For a multi-class classification, we can use for Cross-Entropy this formula:
$$
CE = - \frac{1}{n} \sum_{i=1}^{n} \sum_{j=1}^{K} \mathbb{1} \{y_i = y_j\} \log( P(Y_i = y_j \mid X_i = x_i; \theta) )
$$
where:
- $y_i,\ i = 1, \ldots, n$ - True class for the $i$-th data sample out of all the $n$ samples
- $\mathbb{1} \{y_i = y_j\}$ - Indicator function which equals to 1 when $y_i = y_j$, otherwise 0
- $y_j,\ j = 1, ..., K$ - Represents all the possible classes
- $P(Y_i = y_j \mid X_i = x_i; \theta)$ - Conditional probability that given data sample $x_i$ belongs to the class $y_j$ under parameters $\theta$. From assumptions, it is the $j$-th element from the $f_\theta(x_i)$ - output of the evaluated model for the input $x_i$.

That's because
$$
\Large
\begin{align}
& p_{Y_i \mid X_i}(y \mid x_i; \theta) = \prod_{j=1}^K P(Y_i = y_j \mid X_i = x_i; \theta)^{ \mathbb{1} \{y = y_j\} } \\
& \log( p_{Y_i \mid X_i}(y \mid x_i; \theta) ) 
= \sum_{j=1}^K \mathbb{1} \{y = y_j\} \log( P(Y_i = y_j \mid X_i = x_i; \theta) )
\end{align}
$$
As described in the here - [[Conditional probability distribution function - Discrete random variables#Creating probability mass function formula using probabilities|link]] in the section 'Creating probability mass function formula using probabilities'.
## Binary classification
In case of a binary classification, where we have only two possible classes (0 and 1), for Cross-Entropy we can use this formula:
$$
\large
CE = - \frac{1}{n} \sum_{i=1}^{n} [ y_i \log(p(x_i)) + (1 - y_i) \log(1 - p(x_i)) ]
$$
where:
- $y_i \in \{0, 1\},\ i = 1, \ldots, n$ - True class for the $i$-th data sample out of all the $n$ samples 
- $p(x_i) = P(Y_i = 1 \mid X_i = x_i; \theta)$ - Conditional probability that given data sample $x_i$ belongs to the class $y_j$ under parameters $\theta$. From assumptions, it is the $j$-th element from the $f_\theta(x_i)$ - output of the evaluated model for the input $x_i$.

That's because:
$$
\large
\begin{align}
 & p_{Y \mid X}(y \mid x; \theta) = p(x)^{y}(1 - p(x))^{(1 - y)} \\
 & \log(p_{Y \mid X}(y \mid x; \theta)) = y \log(p(x)) + (1 - y)\log((1 - p(x))
\end{align}
$$
As described in the here - [[Conditional probability distribution function - Discrete random variables#Creating probability mass function formula using probabilities|link]] in the section 'Creating probability mass function formula using probabilities'.

#MachineLearning 