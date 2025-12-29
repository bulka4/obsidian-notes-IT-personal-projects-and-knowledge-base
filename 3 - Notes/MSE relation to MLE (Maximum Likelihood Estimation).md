Tags: [[_Probability]]

# Introduction
MSE (Mean Squared Error) is a loss function ([[MSE (Mean Squared Error)|link]]) for regression models.

MSE formula is derived from using Maximum Likelihood Estimation (MLE) for continuous random variables. Minimalizing the MSE is equivalent to maximizing the likelihood function.
# MSE relation to MLE
## Assumptions
Let's assume, that:
- Machine learning model is a parametric function $f_\theta:\ \mathcal{X} \rightarrow \mathcal{Y}$ as described here - [[What is a Machine Learning model|link]].
- We have a dataset $D = \{ (x_i, y_i) \}_{i=1}^n$ with observations of random variables $X_i, Y_i$ as described here - [[Dataset of observations of random variables X, Y - Variables per sample, feature and target variable|link]]. It will be used for training the model.
- Each $Y_i$ is independent given $\large X_{1:n}$, $Y_i$ depends only on the corresponding $X_i$ and $Y_i$ are identically distributed as described here - [[Independency of random variables|link]].

Let's also assume, that conditional probability distribution $Y_i \mid X_i$ depends on the model. If we assume, that there is a relation between random variables like that: 
$$
Y_i = f_\theta(X_i) + \epsilon_i,\ \epsilon_i \sim \mathcal{N}(0, \sigma^2)
$$
where:
  - $f_\theta$ is our model, for example a Linear Regression or Neural Network

then that gives us the conditional probability distribution of $Y_i \mid X_i$:
$$
Y_i \mid X_i \sim \mathcal{N} (f_\theta(X_i), \sigma^2)
$$
where value of the condition $X_i$ is fixed (known), so value $f_\theta(X_i)$ is also fixed. 

So that means, that once we know value of $X_i$, and:
- We make a prediction $f_\theta(X_i)$ 
- We start observing realizations of $Y_i$ corresponding to that value of $X_i$ 
then mean of those realizations of $Y_i$ will be close to $f_\theta(X_i)$ and variance will be $\sigma^2$ .

And the density function is:
$$
\Large
p_{Y_i \mid X_i}(y | x; \theta) = \frac{1}{ \sqrt{2 \pi \sigma^2} }\exp(
-\frac{ (y - f_\theta(x)) ^ 2 }{2 \sigma^2})
$$
and $\theta = (W, \sigma^2)$.
## Using MLE
The likelihood function formula is (thanks to the variables independency):
$$
\Large
L(\theta) = p_{Y_{1:n} \mid X_{1:n}}(y_{1:n} \mid x_{1:n}; \theta)
= \prod_{i=1}^n p_{Y_i \mid X_i}(y_i \mid x_i; \theta)
$$
So with our assumptions, that is:
$$
L(W, \sigma^2) =  \prod_{i=1}^n \frac{1}{ \sqrt{2 \pi \sigma^2} }\exp(
-\frac{ (y_i - f_\theta(x_i)) ^ 2 }{2 \sigma^2})
$$
where $y_i, x_i$ are known observations of random variables $Y_i, X_i$ from the dataset.

And log-likelihood function formula is:
$$
l(W, \sigma^2) = \log(L(W, \sigma^2)) = -\frac{n}{2} \log(2 \pi \sigma^2)
- \frac{1}{2 \sigma^2} \sum_{i=1}^n (y_i - f_\theta(x_i))^2
$$
Maximizing the likelihood function is equivalent to maximizing this log-likelihood function. Since the first term doesn't depend of $f_\theta$, this is equivalent to minimizing the sum of squared errors:
$$
\hat{W}_{MLE} = \text{arg} \min_W \sum_{i=1}^n (y_i - f_\theta(x_i))^2
$$
if we assume that $\sigma$ is fixed.

In general, in MLE we maximize the likelihood function with respect to all its parameters. In the above formula for $\hat{W}_{MLE}$ we don't include the parameter $\sigma$ because of the assumption that it is fixed.

#Probability 