Tags: [[__Machine_Learning]]

# Introduction
Naive Bayes is a model for mainly classification but it can be also used for regression. In this document we will explain how it works for classification.

It is derived from the Bayes theorem ([[Bayes theorem|link]]).

It classifies data samples based on how likely (popular) are features of that data sample, among different classes.

For example, if we want to predict person's age range based on their height, which is 1 meter, and we know that:
- For age range 0 - 10, height 1 meter is very likely (popular)
- For age range 11 - 20, height 1 meter is very unlikely (unpopular)

Then using Naive Bayes, we would predict for that person the age range 0 - 10, because their height (1 meter), is much more likely for that class.
# The main idea
Let's assume, that:
- $C$ - Random variable ([[Random variable|link]]) representing a class which we want to predict for a given data sample with a set of possible values $\{C_k\}_{k=1}^K$ 
- $\large X_{1:n} = \{X_i\}_{i=1}^n$ - Multivariate random variable ([[Multivariate random variable|link]]) representing features based on which we will be predicting class $C$ 

Naive Bayes uses the Bayes theorem and assumes that features are independent given the class:
$$
P(\bigwedge_{i=1}^n X_i = x_i \mid C = C_k) = \prod_{i=1}^n P(X_i = x_i \mid C = C_k)
$$
This is so called 'Naive' assumption.

Predictions are made by choosing a class $\hat{C}$ which is the most probable one given the set of known observations of the features random variable $\large X_{1:n} = x_{1:n}$, that is:
$$
\large
\hat{C} = \text{arg} \max_{C_k} P(C = C_k \mid \bigwedge_{i=1}^n X_i = x_i)
$$
Using the Bayes theorem, the above equation is equivalent to:
$$
\large
\hat{C} = \text{arg} \max_{C_k} P(C = C_k) \prod_{i=1}^n P(X_i = x_i \mid C = C_k)
$$
Usually, we maximize the logarithm of the above formula:
$$
\large
\hat{C} = \text{arg} \max_{C_k} \left[ \log(P(C_k)) + \sum_{i=1}^n \log(P(X_i = x_i \mid C = C_k)) \right]
$$

We maximize the log because:
- It is simpler because now we have a sum instead of a product (calculating derivatives is simpler)
- That gives the same solution, because $\large \max_x f(x) = \max_x \log(f(x))$

And now we need to calculate somehow $P(C = C_k)$ and $P(X_i = x_i \mid C = C_k)$.

In order to calculate $P(X_i = x_i \mid C = C_k)$, we assume what is a probability distribution of each feature $X_i$ conditioned on the class.

Different choices of this conditional distribution lead to different variants of Naive Bayes:
- Gaussian Naive Bayes
- Multinomial Naive Bayes
- Bernoulli Naive Bayes

In this document, we will focus on the Gaussian version. In that case, we have:
$$
\large
\begin{gather}
X_i \mid C_k \sim \mathcal{N}(\mu_{ik}, \sigma_{ik}^2) \\
P(X_i = x_i \mid C = C_k) = \frac{1}{\sqrt{2 \pi \sigma_{ik}^2}}
\exp \left( -\frac{(x_i - \mu_{ik})^2}{2\sigma_{ik}^2} \right)
\end{gather}
$$

The next section 'Training Naive Bayes' describes how to calculate probabilities $P(C = C_k)$ and $P(X_i = x_i | C = C_k)$.
# Training Naive Bayes
To train Naive Bayes model, we need to calculate values $P(C = C_k)$ and $P(X_i = x_i \mid C = C_k)$.

As mentioned earlier, we assume the Gaussian distribution for $X_i \mid C_k$. We just need to find parameters of that distribution $\large \mu_{ik}, \sigma_{ik}$.

Let's assume, that we have a training dataset $D$ with observations of random variables like described here - [[Dataset of observations of random variables X, Y - Variables per sample, feature and target variable]]. Variable $Y$ from those assumptions correspond to the variable $C$ in this document.
## Class prior (estimating $P(C = C_k)$)
We make an assumption about how probabilities $P(C = C_k)$ look like:
$$
P(C = C_k) = \frac{\text{Number of samples with class } C_k}{\text{Total number of samples}}
$$
where 'number of samples' refers to the training dataset $D$.

Those probabilities $P(C_k)$ are called **class prior**.
## Estimating $P(X_i = x_i \mid C = C_k)$
To estimate $P(X_i = x_i \mid C = C_k)$, we will use Maximum Likelihood Estimation (MLE) ([[Maximum Likelihood Estimation (MLE)|link]]).

For each class $C_k$, we are estimating $P(X_i = x_i \mid C = C_k)$ using only data samples corresponding to that class, that is:
$$
\large
\begin{align}
 & x_{I_k} = (x_{i_1}, \ldots, x_{i_{N_k}}) \\
 & I_k = \{i_1, \ldots, i_{N_k}\}
\end{align}
$$
where:
- $I_k$ is a set of indexes for data samples corresponding to the class k. There is $N_k$ indexes in $I_k$.
- Values $\large x_j$ are values of the $i$-th feature for the $j$-th data sample, which are classified as $C_k$.

To find that maximum of the likelihood function, we will maximize the log-likelihood function, that is:
$$
\large
l(\mu, \sigma^2) = -\frac{N_k}{2} \log(2 \pi \sigma^2)
-\frac{1}{2 \sigma^2} \sum_{j=1}^{N_k} (x_j - \mu)^2
$$
because calculations for finding maximum are easier than in case of likelihood.

To find maximum of $l(\mu, \sigma^2)$, we calculate its derivatives:
$$
\large 
\begin{align}
 & \frac{\partial l}{\partial \mu} (\mu) = -\frac{1}{\sigma^2} 
\sum_{j=1}^{N_k} (x_j - \mu) \\
 & \frac{\partial l}{\partial \sigma^2} (\sigma^2) = -\frac{N_k}{2\sigma^2}
 + \frac{1}{2(\sigma^2)^2} \sum_{j=1}^{N_k} (x_j - \mu)^2
\end{align}
$$
and we calculate such values for $\mu$ and $\sigma^2$, for which those derivatives equal to zero, that is:
$$
\large
\begin{align}
 & \mu = \frac{1}{N_k} \sum_{j=1}^{N_k} x_j \\
 & \sigma^2 = \frac{1}{N_k} \sum_{j=1}^{N_k} (x_j - \mu)^2
\end{align}
$$
Those values can be either a maximum or a minimum of $l(\mu, \sigma^2)$. 

If we calculate second derivatives, we will see that they are lower than zero at those values of $\mu$ and $\sigma^2$, so that means that those values are maximum of the log-likelihood function.
# Interpretation
We make predictions using the formula:
$$
\large
\hat{C} = \text{arg} \max_{C_k} P(C = C_k) \prod_{i=1}^n P(X_i = x_i \mid C = C_k)
$$
Here we have two components:
- $P(C = C_k)$ - How frequent is the $C_k$ class in the dataset
- $P(X_i = x_i \mid C = C_k)$ - How likely (popular) is given feature value $x_i$ among data samples which belong to the class $C_k$.
	- If that probability is high, it votes for classifying the the data sample as $C_k$ 
	- If that probability is low, it votes against classifying the the data sample as $C_k$ 

For example, if we want to predict person's age range based on their height, and:
- For age range 0 - 10, probability distribution of height looks like the blue graph (On the x-axis we have meters)
- For age range 11 - 20, probability distribution of height looks like the red graph
![[2 - Images/Naive bayes/Screenshot 1.png]]

If a person has heigh 1 meter, then:
- $P(\text{height} = 1 \mid \text{age} = [0 - 10])$ is high
- $P(\text{height} = 1 \mid \text{age} = [11 - 20])$ is low

Using Naive Bayes, we would predict for that person the age range [0 - 10], because that person's height (1 meter) is much more likely (popular) among people in that class.

#MachineLearning 