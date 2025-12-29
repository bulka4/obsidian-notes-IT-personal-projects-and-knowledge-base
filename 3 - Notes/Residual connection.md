Tags: [[__Machine_Learning]]

# Introduction
Residual connection is a technique used in neural networks ([[Neural Network|link]]). 

It helps with the vanishing gradients problem and changes how a chosen layer in our neural network works - instead of modifying the input, it adds new information to it.
# How it works
Let's assume, that we have a layer in our neural network which takes an input $X$ and produces output $Y$:
$$
Y = \text{Layer}(X)
$$

Adding a residual connection to that layer means, that we modify output of that layer by adding the input $X$ to it. 

So the final output of the layer with a residual connection becomes:
$$
Y = (X + \text{Layer}(X))
$$

So this way, the layer doesn't transform the input but it adds some additional information to it. 

It is commonly used for example in the Transformer model and is often combined with a layer normalization ([[Neural Network - Layer Normalization|link]]).
# Helping with gradients
Residual connection helps with the vanishing gradients problem ([[Vanishing - exploding gradients|link]]) because when we use a residual connection to calculate the output $Y$:
$$
Y = X + F(X)
$$
and $X$ is an output from the previous layer in our neural network, then to optimize the model we need to know the gradient of the loss function $L$ w.r.t. the input $X$ is, which is:
$$
\large
\nabla_X L = J_X^T (Y) \nabla_Y L = \left( J_X(X) + J_X (F) \right)^T \nabla_Y L 
= \left( I + J_X (F) \right)^T \nabla_Y L
$$
So that means that even if $J_X(F)$ is very small, then $\nabla_X L$ is still similar to $\nabla_Y L$, so it will not be very small (will not vanish).

#MachineLearning 