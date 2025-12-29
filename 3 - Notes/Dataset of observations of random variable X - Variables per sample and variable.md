Tags: [[__Machine_Learning]]

# Introduction
Let's assume, we have a dataset consisting of feature and target variables like described here - [[Features and target variables|link]]:
$$
\large 
D = \{x_1, \dots, x_n\} = \{x_i\}_{i=1}^n
$$
where:
- $\large x_i = (x_{i1}, \dots, x_{im})$ - Features and target variables of the $i$-th data sample

This document explains how to describe that dataset as observations of a multivariate random variable X ([[Multivariate random variable|link]]) of different types ([[Types of random variables|link]]), where we have separate variables per:
- Sample
- Feature
- Target variable
# Notation and shorthands
This document uses notation and shorthands which are described here - [[Mathematical general notations and shorthands|link]].
# Dataset of observations of random variables per sample, feature and target variable
A dataset:
$$
\large 
D = \{x_i\}_{i=1}^n
$$
is a set of observations of a multivariate random variables (discrete, continuous or mixed):
$$
\large
X_{1:n} = (X_1, ..., X_n): (\Omega, \mathcal{F}) \rightarrow (\prod_{i=1}^n \mathcal{X}_i,\ \bigotimes_{i=1}^n \mathcal{B}_{\mathcal{X}_i})
$$
where:
- $X_i$ - Represents a feature or a target variable of the $i$-th sample
- $x_i \in \prod_{j=1}^m \mathcal{X}_{ij}$ is an observation of the random variable $X_i$ 
- $x_i = (x_1, \ldots, x_m)$ represents features and target variables of a single data sample

The dataset $D$ can be also denoted using multivariate random variables ([[Multivariate random variable|link]]) this way:
$$
\large
D = (X_{1:n}) = (X_1, \dots, X_n)
$$

Each component variable also can be multivariate:
$$
\large
X_i = (X_{i1}, \ldots, X_{im}): (\Omega, \mathcal{F}) \rightarrow (\prod_{j=1}^m \mathcal{X}_{ij},\ \bigotimes_{j=1}^m \mathcal{B}_{\mathcal{X}_{ij}})
$$
Representing multiple features and target variables we want to predict:
- $X_{ij}$ - The $j$-th feature or target variable of the $i$-th data sample
# Explanations and Terminology
For more explanations of the above assumptions, refer to the document here - [[Dataset of observations of random variables - Explanation]]

#MachineLearning 