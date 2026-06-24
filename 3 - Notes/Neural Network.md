Tags: [[__Machine_Learning]]

# Introduction
Neural Network is a function:
$$
f: X \rightarrow Y
$$
which takes as an input features and outputs a prediction. It tries to approximate the real function representing a relation between given features and target variable.

It is a composition of many other functions, called layers:
$$
f = f_L \circ \dots \circ f_1
$$
Because of that, it can produce very complex nonlinear functions

So each layer $f_l$ takes a tensor ([[Tensor|link]]) as an input and produces another tensor as an output, which is passed to another layer $f_{l+1}$. Those tensors can have different number of dimensions, depending on the type of the layer. 

Each layer might consist of trainable parameters (but doesn't have to).

Below we can find different types of layers with links to documents explaining them in more detail:
- Fully-connected (dense) - [[Neural Network - Fully-connected (dense) layer|link]]
- Convolution - [[Neural Network - Convolution layer|link]]
- Pooling - [[Neural Network - Pooling layer|link]]
- Recurrent - [[Neural Network - Recurrent layer|link]]
- Attention - [[Neural Network - Attention layer|link]]
- Normalization
# Benefits
- Can model very complex relationships
- Automatic feature learning - It can learn extracting features on its own. Output of each layer can represent features.
- Works for many data types (images, text, time series)
- Scales with data well - more data used for training usually gives better performance
# Drawbacks
- Requires a lot of data
- Hard to interpret
- Computationally expensive
- A lot of hyperparameters to set up (architecture (layers, neurons), learning rate, optimizer, batch size etc.)
- Sensitive to training setup - Performance depends a lot on: initialization (of model parameters like weights), normalization, learning rate.
- Can overfit easily (regularization ([[Regularization|link]]), dropout ([[Neural Networks - Dropout|link]]), weight decay ([[L2 Regularization (Ridge)|link]]) or early stopping ([[Machine Learning - Early stopping|link]]) can help)
# Training 
To train a neural network, consisting of any types of layers, we need to choose a loss function ([[Loss functions|link]]) and use an optimizer (e.g. gradient descent ([[Gradient Descent - ML|link]]) or Adam) to calculate, how to change parameters (weights and biases), to reduce value of a loss function.
## Backpropagation
Backpropagation is an algorithm for efficient calculation of gradients needed for an optimizer (e.g. gradient descent ([[Gradient Descent - ML|link]]) or Adam).

It doesn't just apply a chain rule to calculate all the derivatives, but it reuses derivatives calculated once to calculate further derivatives what saves a lot of time.

How it works is described here - [[Backpropagation (Dense layers)]].

#MachineLearning 