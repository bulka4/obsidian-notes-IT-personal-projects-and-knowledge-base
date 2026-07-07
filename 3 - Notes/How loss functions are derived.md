Tags: [[__Machine_Learning]]
#MachineLearning 

# Introduction
Loss functions are chosen in such a way, that minimalizing it is equivalent to one of the learning methods:
- Maximizing the likelihood (Maximum Likelihood Estimation (MLE))
	- More information here - [[Maximum Likelihood Estimation (MLE)|link]] 
	- Maximizing probability of observing given realizations of random variables 
- Minimizing a divergence or distance between probability distributions 
	- More information here - [[Minimizing divergence between probability distributions|link]] 
	- e.g., Kullback–Leibler divergence, cross-entropy, or other objectives derived from Bayesian or information-theoretic principles;
- Minimizing an expected risk (decision-theoretic loss)
	- The loss represents the cost of prediction errors under a specific utility or margin-based criterion.
- Minimizing a distance in a feature space
	- Encourages relative relationships (similar/dissimilar) rather than exact labels. 
	- Can be interpreted as minimizing an expected “distance-based risk” rather than standard MSE or CE. For example Triplet loss, contrastive loss.

How a loss function looks like is determined by:
- What learning method do we choose (e.g. maximizing likelihood)
- What probability distribution ($p(y | x)$ of the target variable $Y$ given features $X$) our model represents ([[Probability distribution represented by a model|link]])

For example, when we use MLE method, we choose such a loss function that minimizing it is equivalent to maximizing likelihood which is calculated using a probability distribution defined by a model.
# Probability distribution represented by a model
[[Probability distribution represented by a model]].