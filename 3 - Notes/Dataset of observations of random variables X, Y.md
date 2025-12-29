Tags: [[__Machine_Learning]]

# Introduction
Let's assume, that:
- We have a dataset with data points as described here - [[Features and target variables|link]]:
$$
\large 
D = \{(x_1, y_1), \dots, (x_n, y_n)\} = \{(x_i, y_i)\}_{i=1}^n
$$
	where:
	- $\large x_i = (x_{i1}, \dots, x_{id})$ - Features of the $i$-th data sample
	- $\large y_i = (y_{i1}, \dots, y_{ik})$ - Target variables of the $i$-th data sample
- Variables $x_i, y_i$ are already converted into a numeric form as described here - [[Converting categorical variables into numeric ones|link]].

Then, we can look at that dataset as a dataset with observations ([[Observations - realizations of random variables|link]]) of a multivariate random variables X and Y ([[Multivariate random variable|link]]):
$$
\begin{align}
& X = (X_1, \dots, X_n) \\
& Y = (Y_1, \dots, Y_n)
\end{align}
$$
where components $X_i, Y_i$ of those variables can be variables of different types ([[Types of random variables|link]]) representing data samples.

There are different ways how we can represent those numbers as observations of random variables:
- [[Dataset of observations of random variables X, Y - Variables per sample, feature and target variable]]
- [[Dataset of observations of random variables X, Y - Variables per feature and target variable]]
# Additional explanation
Additional explanation regarding representing that dataset as observations of random variables can be found here - [[Dataset of observations of random variables - Explanation]].

#MachineLearning 