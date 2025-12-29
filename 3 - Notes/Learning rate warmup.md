Tags: [[_Mathematical_analysis]]

# Introduction
When using gradient-based optimization algorithms, like gradient descent ([[Gradient Descent - ML|link]]) or Adam ([[Adam optimizer|link]]), at the beginning of training an ML model ([[Training machine learning models - Introduction|link]]):
- Model's weights are randomly initialized
- Gradients can be large and unstable
- Optimizer statistics (e.g., Adam’s moments) are unreliable

Using a full learning rate immediately can:
- Cause huge parameter updates
- Lead to loss spikes or NaNs
- Destabilize training

Warmup prevents this by starting with a smaller learning rate and increasing it in further optimization steps.

#MathematicalAnalysis 