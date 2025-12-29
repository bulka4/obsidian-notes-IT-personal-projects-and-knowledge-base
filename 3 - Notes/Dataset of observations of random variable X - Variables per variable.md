Tags: [[__Machine_Learning]]

# Introduction
Let's assume, we have a dataset consisting of feature and target variables like described here - [[Features and target variables|link]]:
$$
\large 
D = \{x_1, \dots, x_n\} = \{x_i\}_{i=1}^n
$$
where:
- $\large x_i = (x_{i1}, \dots, x_{im})$ - Features and target variables of the $i$-th data sample

This document explains how to describe that dataset as observations of multivariate random variable X ([[Multivariate random variable|link]]) of different types ([[Types of random variables|link]]), where we have separate variables per:
- Feature
- Target variable
# Notation and shorthands
This document uses notation and shorthands which are described here - [[Mathematical general notations and shorthands|link]].
# Dataset assumptions
A dataset:
$$
\large 
D = \{x_i\}_{i=1}^n
$$
is a set of observations of a multivariate random variables (discrete, continuous or mixed):
$$
\large
X_{1:m} = (X_1, ..., X_m): (\Omega, \mathcal{F}) \rightarrow (\prod_{i=1}^m \mathcal{X}_i,\ \bigotimes_{i=1}^m \mathcal{B}_{\mathcal{X}_i})
$$
where:
- $X_i$ - Represents the $i$-th feature or target variable
- $x_{ij} \in \mathcal{X}_{j}$ is the $i$-th observation of the random variable $X_j$ ($j$-th feature or target variable)
# Explanations and Terminology
For more explanations of the above assumptions, refer to the document here - [[Dataset of observations of random variables - Explanation]]

#MachineLearning 