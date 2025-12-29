Tags: [[__Machine_Learning]]

# Introduction
Fully-connected (dense) layer consist of neurons which performs a linear operation on the input, and output of that linear operation is passed into a non-linear activation function.
## Neurons
Neuron is a function:
$$
\text{neuron}(x) = \sigma(w^Tx + b)
$$
where:
- $x$ - Input vector
- $w$ - Weights
- $b$ - bias
- $\sigma$ - Activation function (e.g. ReLU, sigmoid, tanh)

Weights and biases are trainable model parameters.

Activation function squishes the result of the linear equation $w^Tx + b$ to smaller values, for example to a number from the range [0, 1], to represent a probability.
## Dense layer
A dense layer takes a vector as an input and passes it to multiple neurons.

Each neuron in a dense layer, takes as an input the same, entire vector, which is an input for the entire layer.

Each neuron outputs a number. So output of the entire layer is a vector, which length equals to number of neurons.

If we have multiple dense layers one after another, then output from all the neurons from one layer, is an input for each neuron in another layer.

Set of dense layers look like that:
![[2 - Images/Neural Network/Screenshot 1.png]]

Every layer can contain any number of neurons (3 neurons per layer in the picture is just an example).
# Dense layer described mathematically
In order to see, how to describe mathematically how a dense layer works:
- What functions and variables we have
- What calculations are performed to produce an output

refer to this document - [[Neural Network - Dense layer described mathematically]].
# Why we add a bias
Let’s assume that our network consists of only one node and activation function is relu function. 

If in our dataset we have an example where input x = 0 and corresponding y = 2, then no matter what weights we choose, the output of a node will be 0, because:
$$
\text{relu}(w^T0) = \text{relu}(0) = 0
$$
So we will never get 2 as the output.
# Interpretation
We can interpret, that each neuron an layer is extracting different kind of information from the input.

#MachineLearning 