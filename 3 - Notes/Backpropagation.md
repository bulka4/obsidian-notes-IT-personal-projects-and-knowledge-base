Tags: [[__Machine_Learning]]

# Introduction
Backpropagation is used to calculate efficiently derivatives in neural network needed to use an optimizer (e.g. gradient descent ([[Gradient Descent - ML|link]]) or Adam) to train it (update its parameters to reduce loss).

It doesn't just apply a chain rule to calculate all the derivatives separately, but it reuses calculated derivatives to calculate further derivatives what saves a lot of time.
# Backpropagation for a dense layer
This document describes how backpropagation works in case of a set of dense layers - [[Backpropagation (Dense layers)]].

#MachineLearning 