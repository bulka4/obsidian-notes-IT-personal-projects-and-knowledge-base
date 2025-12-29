Tags: [[__Machine_Learning]]

# Introduction
This document describes mathematically how dense layer works:
- What functions and variables we have
- What calculations are performed to produce an output
# Notation, variables and functions
We have $L$ layers.

We have functions:
- $f^{(l)}$ - Activation function for the $l$-th layer

And variables:
- $a^{(l)}$ - $l$-th layer activations
	- Output from activation functions from the $l$-th layer
	- $a^{(0)}$ is the input for the model
	- $a^{(L)}$ is model's prediction (final layer)
- $z^{(l)}$ - $l$-th layer pre-activation (linear part)
	- Output from the linear equation which is an input for an activation function
- $W^{(l)}$ - Weights from the $l$-th layer
- $b^{(l)}$ - Biases from the $l$-th layer

So we have:
$$
\large
\begin{align}
 & z^{(l)} = W^{(l)} a^{(l - 1)} + b^{(l)} \\
 & a^{(l)} = f^{(l)}(z^{(l)}) \\
 & g = f^{(L)} \circ z^{(L)} \circ f^{(L - 1)} \circ z^{(L - 1)} \circ \ldots \circ f^{(1)} \circ z^{(1)} \circ f^{(0)}
\end{align}
$$
where $g$ represents the entire neural network which is a composition of activation functions from each layer.
# Shapes of variables
Let's denote as $n_l$ a number of neurons in the $l$-th layer ($n_0$ represents length of the input vector). Then shapes of variables are:
$$
\large
\begin{align}
W^{(l)}: & (n^{(l)}, n^{(l-1)}) \\
b^{(l)}: & (n^{(l)}, 1) \\
a^{(l)}: & (n^{(l)}, 1) \\
z^{(l)}: & (n^{(l)}, 1) \\
\end{align}
$$
We interpret those matrices as follows:
- Each row in every matrix represents a neuron
- Each row in the weights matrix $W^{(l)}$ contains one weight per neuron in the previous layer (or per one element in the input vector)

So when performing calculations for pre-activation:
$$
z^{(l)} = W^{(l)} a^{(l - 1)} + b^{(l)}
$$
shapes change as follows:
$$
\large
\underbrace{(n^{(l)}, n^{(l-1)})}_{W^{(l)}} 
\cdot \underbrace{(n^{(l-1)}, 1)}_{a^{(l-1)}}
+ \underbrace{(n^{(l)}, 1)}_{b^{(l)}} = 
	(n^{(l)}, 1) + (n^{(l)}, 1) = (n^{(l)}, 1)
$$
And for activation we have:
$$
\Large
a^{(l)} = f^{(l)}(z^{(l)}) = 
\begin{pmatrix}
f^{(l)}(z^{(l)}_1) \\
\vdots \\
f^{(l)}(z^{(l)}_{n^{(l)}}) \\
\end{pmatrix}
$$

#MachineLearning 