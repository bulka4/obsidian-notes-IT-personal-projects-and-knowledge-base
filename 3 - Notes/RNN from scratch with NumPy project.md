Tags: [[__My_projects]] [[__Machine_Learning]]
#MyProjects #MachineLearning 

# Introduction
In this project we create and train a LSTM ([[Neural Network - LSTM layer|link]]) and recurrent neural network ([[Neural Network - Recurrent layer|link]]) from scratch using only NumPy library, i.e. we program all the mathematical operations on our own:
- Calculating model output and loss
- Calculating gradients
- Updating model's parameters using gradients
# Project code repository
A repository with a code for this project is here - [github.com](https://github.com/bulka4/rnn_from_scratch).
# Backpropagation
We don't use here a proper backpropagation where we reuse gradients calculated once to calculate another gradients. Instead, we calculate the same gradients multiple times.

A proper backpropagation for a Dense layer is described here - [[Backpropagation (Dense layers)]].
# Vanishing gradient
There is a problem with a vanishing gradient. It is very small (around 10 ** -70) and it is being rounded to 0.

Possible solutions might be:
- Gradient clipping ([[Gradient control - Gradient clipping|link]]) - setting max and min threshold for all derivatives
- Use layer normalization ([[Neural Network - Layer Normalization|link]])
# Caffe2 library for faster calculations
We can use the Caffe2 library for faster calculations.
# Useful materials
Additional, useful materials about this topic:
- [github.com](https://github.com/bulka4/Useful_materials/tree/main/Recurrent%20Neural%20Networks) 