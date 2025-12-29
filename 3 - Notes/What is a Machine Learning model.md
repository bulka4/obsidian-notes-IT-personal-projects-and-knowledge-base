Tags: [[__Machine_Learning]]

# Introduction
Machine Learning model is a function which consists of parameters and it is used to predict a value of a target variable $Y$ based on a set of features $X$ ([[Dataset of observations of random variables X, Y - Variables per sample, feature and target variable|link]]).

It is denoted as:
$$
f_\theta : \mathcal{X} \rightarrow \mathcal{Y}
$$
where:
- $\mathcal{X}$ - Input space containing vectors representing features
- $\mathcal{Y}$ - Output space containing vectors representing predictions of a target variable
- $\theta$ - Model parameters

An example of a Machine Learning model is Linear Regression which is a linear function:
$$
f_\theta(x) = w_0 + w_1 x_1 + ... + w_n x_n
$$
where:
- $\theta = \{w_i\}_{i=0}^n$ - Model parameters
- $x = \{x_i\}_{i=0}^n$ - Input

Model can be used for example to predict a price of a house based on its features. In that case $x \in \mathcal{X}$ represents house features, such as its area, number of bathrooms etc., and $f_\theta(x) = y \in \mathcal{Y}$ represents predicted price of that house.

#MachineLearning 