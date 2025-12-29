Tags: [[__Machine_Learning]]

# Introduction
KL Divergence can be used for training statistical models. It works in the following way:
- We have a model which is a parametric function $f_\theta$, where $\theta$ are parameters ([[What is a Machine Learning model|link]])
- Cross-Entropy ([[Cross-Entropy|link]]) value depends on model's parameters $\theta$ 
- KL Divergence value depends on Cross-Entropy ([[Relation between KL Divergence and Cross-Entropy and Entropy|link]]). Lower Cross-Entropy implies lower Divergence.
- We find such a parameters for the model, which minimizes KL Divergence, using for example gradient descent algorithm ([[Gradient Descent - ML|link]])

As described here - [[KL Divergence]], we minimize KL Divergence because lower value indicates that probability distribution defined by our model is similar to the true distribution of random variables which generated given dataset.
# How to use KL Divergence for training models
KL Divergence helps us to measure the divergence (difference) between the true probability distribution $p$ and the one defined by the statistical model $q_\theta$.

We can train a model in such a way, as to minimize the KL Divergence, thus minimizing the difference between probability distributions. 

Since KL Divergence is given by the formula:
$$
\large
D_{KL}(p \lVert q_\theta) = 
-\mathbb{E}_{P(Y \mid X = x)} (\log(q_\theta(Y \mid x))) - 
(-\mathbb{E}_{P(Y \mid X = x)} (\log( p(Y \mid x))))
= H(P, Q) - H(P)
$$
then we can minimize it by minimizing the $H(P, Q)$ value, which is the Cross-Entropy ([[Cross-Entropy|link]]).

That's because only that value depends on the model $q_\theta$ which we control. The other value $H(P)$ can't be calculated (it is only a theoretical value), so we can't minimize it.

To calculate Cross-Entropy, we assume that:
- $D = \{ (x_i, y_i) \}_{i=1}^n$ - Dataset with observations of random variables $X_i, Y_i$ as described here - [[Dataset of observations of random variables X, Y - Variables per sample, feature and target variable|link]]. It will be used for training the model.
- Pairs $(X_i, Y_i)$ are i.i.d. copies of $(X, Y)$ (as described here - [[Independent and identically distributed (i.i.d.) pairs of random variables|link]])
- $p$ - The true probability distribution function ([[Probability distribution (density, mass) function|link]]) of $(X, Y)$ 
- $q = q_\theta$ - Parametric probability distribution defined by a statistical model for $(X_i, Y_i)$ samples of $(X, Y)$ ([[Dataset of observations of random variables - Explanation|link]])
- $p$ and $q = q_\theta$ corresponds to probability distributions $P$ and $Q$ 

Training models by minimizing Cross-Entropy is described here - [[Cross-Entropy for classification]].

#MachineLearning 