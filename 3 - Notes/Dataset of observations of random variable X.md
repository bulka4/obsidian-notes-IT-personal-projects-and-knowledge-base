Tags: [[__Machine_Learning]]

# Introduction
Let's assume, that:
- We have a dataset with data points as described here - [[Dataset used for creating ML models (data points, samples, variables)|link]]:
$$
\large
D = \{x_1, \dots, x_n\} = \{x_i\}_{i=1}^n
$$
	where:
	- $x_i = (x_{i1}, \ldots, x_{im})$ is a data sample with variables $x_{ij}$.
- Variables $x_i$ are already converted into a numeric form as described here - [[Converting categorical variables into numeric ones|link]].

Then, we can look at that dataset as a dataset with observations ([[Observations - realizations of random variables|link]]) of a multivariate random variable X ([[Multivariate random variable|link]]):
$$
X = (X_1, \dots, X_n)
$$
where components $X_i$ of that variable can be variables of different types ([[Types of random variables|link]]) representing data samples.

There are different ways how we can represent those numbers as observations of random variables:
- [[Dataset of observations of random variable X - Variables per sample and variable]]
- [[Dataset of observations of random variable X - Variables per variable]]
# Additional explanation
Additional explanation regarding representing that dataset as observations of random variables can be found here - [[Dataset of observations of random variables - Explanation]].

#MachineLearning 