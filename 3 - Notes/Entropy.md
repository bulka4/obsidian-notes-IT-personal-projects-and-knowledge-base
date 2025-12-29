Tags: [[_Information_theory]], [[__Mathematics]]

# Introduction
Entropy is related to uncertainty of an experiment outcome and surprise measure. We can learn more about them here - [[Experiment outcome uncertainty and average surprise measures]].

Entropy measures an uncertainty of an experiment outcome, how hard it is to predict what will be an outcome of that experiment (how unpredictable a random variable $X$ is).

Also, we can interpret it, that it measures how 'surprised' we are on average when observing outcomes of experiments (observations of a random variable $X$).

Entropy's formula contains the $-log(p(X))$ component which is the surprise measure.

More precisely:
- High Entropy -> outcomes are uncertain, hard to predict and average surprise is high (highest probabilities are distributed across many different outcomes)
- Low Entropy -> outcomes are uncertain, hard to predict and average surprise is high (highest probabilities are distributed across a few different outcomes)
# Definition
Entropy is defined as:
$$
H(X) = \mathbb{E}[-log(p(X))]
$$
where:
- $X$ - Random variable
- $p$ - Probability distribution function of $X$ 
## Discrete random variables
When $X$ is a discrete random variable, then expected value looks like described here - [[Expected value|link]] in the section about discrete random variables, and Entropy formula is:
$$
H(X) = -\sum_{x}p(x) \log[p(x)]
$$
## Continuous random variables
When $X$ is a continuous random variable, then expected value looks like described here - [[Expected value|link]] in the section about continuous random variables, and Entropy formula is:
$$
H(X) = -\int_{\mathbb{R}}p(x) \log[p(x)]\ dx
$$

# Interpretation
More about interpretation of Entropy as a measure of uncertainty and average surprise can be found here - [[Experiment outcome uncertainty and average surprise measures|link]].
# Other related topics
- Decision trees
- Gini impurity
- Dataset diversity measures

#InformationTheory #Mathematics 