Tags: [[__Machine_Learning]]

# Introduction
In context of machine learning, batching is a technique where we process multiple data samples ([[Dataset used for creating ML models (data points, samples, variables)|link]]) at once.

That can be used during inference (making predictions) and training a model ([[Training machine learning models - Introduction|link]]).

All data samples are passed into a model as a single tensor ([[Tensor|link]]), model process all of them in parallel and returns a single tensor with predictions for all the samples.

It makes calculations more efficient on GPUs because we can perform more calculations in parallel.

Also, during training models using gradient-based optimizers like gradient descent ([[Gradient Descent - ML|link]]) or Adam ([[Adam optimizer|link]]):
- Gradients are more stable (it is less likely that gradient will be equal to zero or that it will be very big)
- Training is faster because we calculate loss and gradients once per batch instead of once per sample
# Continuous (dynamic) batching
There is also another version of batching, continuous (dynamic) batching. More information can be found here - [[Continuous (dynamic) batching]].

#MachineLearning 