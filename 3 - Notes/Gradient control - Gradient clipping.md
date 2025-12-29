Tags: [[_Mathematical_analysis]]

# Introduction
Gradient clipping is a method of gradient control ([[Gradient control|link]]) that helps with exploding gradient problem ([[Vanishing - exploding gradients|link]]) and prevents updating model weights too much by limiting the size of gradients. 

Updating weights too much could cause obtaining NaN or Inf values due to finite-precision numeric formats ([[Numeric formats (precision) - Calculation errors|link]]) or that we miss the optimal point (where the loss is minimal).

Two common ways of doing that include:
- Norm clipping
- Value clipping
# Norm clipping
In a norm clipping we modify gradients in the following way:
$$
\large
g_{\text{new}} = g \cdot \frac{\text{max\_norm}}{||g||},\ \text{if } ||g|| > \text{max\_norm}
$$
where:
- $||g||$ is a vector norm ([[Vector norm|link]])
- max_norm is a chosen value (maximal allowed norm)
# Value clipping
In a value clipping we modify gradients in the following way:
$$
\large
g_i^{\text{new}} = \text{clip}(g_i, - c, c)
$$
where:
$$
\text{clip}(x, a, b) = \begin{cases}
a & \text{if } x < a \\
b & \text{if } x > b \\
x & \text{otherwise} \\
\end{cases}
$$

#MathematicalAnalysis 