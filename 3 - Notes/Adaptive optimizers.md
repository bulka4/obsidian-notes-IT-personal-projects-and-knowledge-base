Tags: [[_Mathematical_analysis]]

# Introduction
Adaptive optimizers are gradient-based optimization algorithms that automatically adjust the effective learning rate for each parameter based on the history of gradients.
# Why adaptive optimizers exist
In real models:
- Different parameters get gradients of very different scales
- Gradient magnitudes change during training
- A single global learning rate is often not optimal

Adaptive optimizers handle this automatically.
# How it works
On a high level:
- Parameters with large or noisy gradients (gradients sometimes are big and sometimes small) get smaller updates
- Parameters with small or stable gradients get larger updates

In case of Adam ([[Adam optimizer|link]]), we use this formula for updating parameters:
$$
\large
\theta_{t+1} = \theta_t - \alpha \frac{\hat{m_t}}{\sqrt{\hat{v_t}} + \epsilon}
$$
- Division by $\sqrt{v_t}$​​ rescales gradients
- Each parameter gets its own effective learning rate
- Large gradients are damped
- Small gradients are amplified
# Benefits
Adaptive optimizers:
- Reduce sensitivity to gradient scale
	- So parameters are not updated too much by big gradients and too little by small ones
- Help with exploding and vanishing gradients (partially)
- Work well with sparse or noisy gradients (gradients which have many zeros or sometimes are big and sometimes small)
- Are robust in mixed precision
	- Model parameters are less likely to become NaN on Inf due to finite-precision numeric formats ([[Numeric formats (precision) - Calculation errors|link]]) since big gradients has reduced impact

#MathematicalAnalysis 