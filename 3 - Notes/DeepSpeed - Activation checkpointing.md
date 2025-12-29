Tags: [[__Distributed_computing]], [[__Machine_Learning_Engineering]]

# Introduction
Normally, when we train a neural network ([[Neural Network|link]]):
- During a forward pass (calculating model's output), we store all the activations (outputs of activation functions)
- Then, we use saved activations during backpropagation ([[Backpropagation (Dense layers)|link]]) to calculate gradients and optimize model parameters using for example gradient descent ([[Gradient Descent - ML|link]])

Using activation checkpointing, only some of the activations are saved during forward pass and reused during backpropagation, while others are recomputed.

It allows to save memory but computation is slower (we need to recompute activations additionally).

That allows to train bigger models and use bigger batch sizes.

#DistributedComputing #MLEngineering 