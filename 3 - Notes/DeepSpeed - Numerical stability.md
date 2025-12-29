Tags: [[_DeepSpeed]], [[__Machine_Learning_Engineering]]

# Introduction
Numerical stability is about making sure computations behave well, when using numeric formats ([[Numeric formats (precision)|link]]) like FP16, BF16, FP32. Especially when values get very large, very small, or repeatedly accumulated. 

So we don't get problems like vanishing / exploding gradients in gradient-based optimizers like gradient descent ([[Gradient Descent - ML|link]])

When performing calculations on numbers represented using numeric formats, they are not perfect. There are some errors as numbers are not represented super precisely ([[Numeric formats (precision) - Calculation errors|link]]).

There are different ways for assuring numerical stability:
- Stable softmax
- Log-sum-exp trick
- Mixed precision stability tools
# Accumulation error
When performing calculations on numbers represented using numeric formats, they are not perfect. There can happen small errors like described here - [[Numeric formats (precision) - Calculation errors|link]].

If we perform many operations (adding, multiplying), those errors accumulate and become significant.

Accumulation error is most severe during summation, because rounding occurs at every addition and floating-point addition is not associative.
# Stable softmax
Instead of calculating:
$$
\large \frac{\exp(x_i)}{ \sum_{j} \exp(x_j) }
$$
we calculate:
$$
\large \frac{\exp(x_i - m)}{ \sum_{j} \exp(x_j - m) }, \quad m = \max_j x_j
$$
# Log-sum-exp trick
Instead of calculating:
$$
\large \log \sum_i e^{x_i}
$$
we calculate:
$$
\large m + \log \sum_i e^{x_i - m}, \quad m = \max_i x_i
$$
Prevents overflow. This is commonly used in log-likelihoods and attention mechanisms.
# Mixed precision stability tools
Multiply loss by a factor to make it bigger, to make gradients bigger (prevents underflow). Then divide gradients.

We use different precisions for different operations:
- Forward pass (calculating output): FP16 / BF16
- Multiplying loss by a factor: FP32
- Backward pass (calculating gradients): FP16 / BF16
- Summing gradients in FP32
- Weights: FP32

#DeepSpeed #MLEngineering 