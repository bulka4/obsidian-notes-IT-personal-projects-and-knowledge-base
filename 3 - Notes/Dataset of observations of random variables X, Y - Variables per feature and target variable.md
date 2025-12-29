Tags: [[__Machine_Learning]]

# Introduction
Let's assume, we have a dataset consisting of feature and target variables like described here - [[Features and target variables|link]]:
$$
\large 
D = \{(x_1, y_1), \dots, (x_n, y_n)\} = \{(x_i, y_i)\}_{i=1}^n
$$
where:
- $\large x_i = (x_{i1}, \dots, x_{id})$ - Features of the $i$-th data sample
- $\large y_i = (y_{i1}, \dots, y_{ik})$ - Target variables of the $i$-th data sample

This document explains how to describe that dataset as observations of multivariate random variables X and Y ([[Multivariate random variable|link]]) of different types ([[Types of random variables|link]]), where we have separate variables per:
- Feature
- Target variable
# Notation and shorthands
This document uses notation and shorthands which are described here - [[Mathematical general notations and shorthands|link]].
# Dataset assumptions
A dataset:
$$
\large 
D = \{(x_i, y_i)\}_{i=1}^n
$$
is a set of observations of multivariate random variables (discrete, continuous or mixed):
$$
\large
\begin{align}
 & Y_{1:k} = (Y_1, ..., Y_k): (\Omega, \mathcal{F}) \rightarrow (\prod_{i=1}^k \mathcal{Y}_i,\ \bigotimes_{i=1}^k \mathcal{B}_{\mathcal{Y}_i}) \\
 & X_{1:d} = (X_1, ..., X_d): (\Omega, \mathcal{F}) \rightarrow (\prod_{i=1}^d \mathcal{X}_i,\ \bigotimes_{i=1}^d \mathcal{B}_{\mathcal{X}_i})
\end{align}
$$
where:
- $X_i$ - Represents the $i$-th feature
- $Y_i$ - Represents the $i$-th target variable
- $x_{ij} \in \mathcal{X}_{j}$ is the $i$-th observation of the random variable $X_j$ ($j$-th feature)
- $y_{ij} \in \mathcal{Y}_j$ is the $i$-th observation of the random variable $Y_j$ ($j$-th target variable)
# Explanations and Terminology
For more explanations of the above assumptions, refer to the document here - [[Dataset of observations of random variables - Explanation]]

#MachineLearning 