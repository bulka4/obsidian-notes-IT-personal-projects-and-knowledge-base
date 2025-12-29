Tags: [[_Mathematical_analysis]]

# Introduction
Gradient normalization is a method of gradient control ([[Gradient control|link]]) that helps with exploding gradient problem ([[Vanishing - exploding gradients|link]]) and prevents updating model weights too much by limiting the size of gradients. 

Updating weights too much could cause obtaining NaN or Inf values due to finite-precision numeric formats ([[Numeric formats (precision) - Calculation errors|link]]) or that we miss the optimal point (where the loss is minimal).

We change gradients by scaling them to a unit norm ([[Vector norm|link]]):
$$
\large g_{\text{new}} = \frac{g}{||g||}
$$

#MathematicalAnalysis 