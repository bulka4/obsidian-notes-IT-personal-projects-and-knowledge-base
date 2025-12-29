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
- Sample
- Feature
- Target variable
# Notation and shorthands
This document uses notation and shorthands which are described here - [[Mathematical general notations and shorthands|link]].
# Dataset of observations of random variables per sample, feature and target variable
A dataset:
$$
\large 
D = \{(x_i, y_i)\}_{i=1}^n
$$
is a set of observations of multivariate random variables (discrete, continuous or mixed):
$$
\large
\begin{align}
 & Y_{1:n} = (Y_1, ..., Y_n): (\Omega, \mathcal{F}) \rightarrow (\prod_{i=1}^n \mathcal{Y}_i,\ \bigotimes_{i=1}^n \mathcal{B}_{\mathcal{Y}_i}) \\
 & X_{1:n} = (X_1, ..., X_n): (\Omega, \mathcal{F}) \rightarrow (\prod_{i=1}^n \mathcal{X}_i,\ \bigotimes_{i=1}^n \mathcal{B}_{\mathcal{X}_i})
\end{align}
$$
where:
- $X_i, Y_i$ - Represents features and target variables of the $i$-th sample
- $x_i \in \prod_{j=1}^d \mathcal{X}_{ij}$ is an observation of the random variable $X_i$ 
- $x_i = (x_{i1}, \dots, x_{id})$ represents $d$ features of a single data sample
- $y_i \in \prod_{j=1}^k \mathcal{Y}_{ij}$ is an observation of the random variable $Y_i$ 
- $y_i = (y_{i1}, \dots, y_{ik})$ represents $k$ target variables of a single data sample

The dataset $D$ can be also denoted using multivariate random variables ([[Multivariate random variable|link]]) this way:
$$
\large
D = (X_{1:n}, Y_{1:n}) = ((X_1, Y_1), \ldots, (X_n, Y_n)) = ((X_i, Y_i)_{i=1}^n) 
$$

Each component variable also can be multivariate:
$$
\large
\begin{align}
& Y_i = (Y_{i1}, \ldots, Y_{ik}): (\Omega, \mathcal{F}) \rightarrow (\prod_{j=1}^k \mathcal{Y}_{ij},\ \bigotimes_{j=1}^k \mathcal{B}_{\mathcal{Y}_{ij}}) \\
& X_i = (X_{i1}, \ldots, X_{id}): (\Omega, \mathcal{F}) \rightarrow (\prod_{j=1}^d \mathcal{X}_{ij},\ \bigotimes_{j=1}^d \mathcal{B}_{\mathcal{X}_{ij}})
\end{align}
$$
Representing multiple features and target variables we want to predict:
- $X_{ij}$ - The $j$-th feature of the $i$-th data sample
- $Y_{ij}$ - The $j$-th target variable of the $i$-th data sample
# Explanations and Terminology
For more explanations of the above assumptions, refer to the document here - [[Dataset of observations of random variables - Explanation]]

#MachineLearning 