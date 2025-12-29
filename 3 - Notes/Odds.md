Tags: [[__Machine_Learning]]

# Unconditional odds
The definition of odds is different for a binary and multi-class classification.

***1. Binary classification***
Odds of an event happening are defined as:
$$
\text{odds} = \frac{p}{1-p}
$$
where $p$ is a probability of an event happening. 

***2. Multi-class classification***
In terms of a multi-class classification, we talk about odds of one outcome relative to another:
$$
\text{odds}_{j/K} = \frac{P(y = j | x)}{P(y = K | x)}
$$
where $K$ is a reference class (i.e. any chosen class).
# Conditional odds
Odds tells us if there is a relationship between 2 binary variables X and Y. We calculate
$$
\text{odds} = \frac{P(X = 1 | Y = 1)}{P(X = 1 | Y = 0)}
$$
or
$$
\text{odds} = \frac{P(X = 0 | Y = 1)}{P(X = 0 | Y = 0)}
$$
Values much bigger or smaller than 1 indicates that there is strong relationship between X and Y. We can use chi-square test, fischer’s exact test or wald test to check if our calculated odds ratio is statisticaly significant.

#MachineLearning  