Tags: [[__Machine_Learning]]

# Introduction
Layer normalization is a technique used in neural networks ([[Neural Network|link]]) which normalizes input for a layer. It is not just a standard normalization because it contains trainable parameters.

It helps with the vanishing / exploding gradients problem ([[Vanishing - exploding gradients|link]]) because it rescales the input for the layer to have a stable mean and variance (mean $\approx$ 0, variance $\approx$ 1). Thanks to that, changing that layer's parameters doesn't make too big nor too small change in the final output (so gradients are not too small nor too big).

This operation is denoted as LayerNorm() and it can be seen as another type of a neural network layer but we usually say 'Layer Normalization'.
# How it works
LayerNorm takes as an input a vector:
$$
\large
x = (x_1, \ldots, x_d)
$$

***1. Calculate mean and variance***
calculates its mean $\mu$ and variance $\sigma^2$ :
$$
\mu = \frac{1}{d} \sum_{i=1}^d x_i, \quad 
\sigma^2 = \frac{1}{d} \sum_{i=1}^d (x_i - \mu)^2
$$

***2. Normalize input vector x***
Then, using those values, it calculates normalized components of $x$:
$$
\large
\hat{x_i} = \frac{x_i - \mu}{\sqrt{\sigma^2 + \epsilon}}
$$
where $\epsilon$ is a small number which prevents dividing by zero.

Normalized vector $\hat{x} = (\hat{x}_1, \ldots, \hat{x_d})$ has mean 0 and variance 1.

***3. Apply learned scale and shift***
LayerNorm uses two trainable parameters per feature:
- $\large \gamma_i$ - Scale
- $\large \beta_i$ - Bias

to generate the final output of the LayerNorm:
$$
\large
y_i = \gamma_i \hat{x_i} + \beta_i
$$

#MachineLearning 