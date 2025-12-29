Tags: [[__Machine_Learning]]

# Introduction
Backpropagation is used to calculate efficiently derivatives in neural network needed to use an optimizer (e.g. gradient descent ([[Gradient Descent - ML|link]]) or Adam) to train it (update its parameters to reduce loss).

It doesn't just apply a chain rule to calculate all the derivatives separately, but it reuses calculated derivatives to calculate further derivatives what saves a lot of time.

This document describes how backpropagation works in case of a set of dense layers ([[Neural Network - Fully-connected (dense) layer|link]]).
# Neural network architecture and notation
In this document, we will use the notation from this document - [[Neural Network - Dense layer described mathematically]], to denote loss, weights, activation functions etc.

That document describes mathematically how neural network works:
- What functions and variables we have
- What calculations are performed to produce an output
# Loss function
We have a loss function which is some function of $a^{(L)}$ (predictions) and $y$ (true values of the target variable):
$$
L = \mathcal{L}(a^{(L)}, y)
$$
It returns a scalar. If it returns a vector, we reduce it to scalar by taking for example a sum or average.
# Goal
The final goal of backpropagation is to find derivatives of the loss w.r.t. weights and biases:
$$
\Large \nabla_{W^{(l)}} L$ \quad \Large \nabla_{b^{(l)}} L
$$
for every layer $l$ .

Then, we can use them in an algorithm like gradient descent for finding such parameters $W^{(l)}$ and $b^{(l)}$, which will minimalize the value of the loss function.
# Derivatives
When we write derivatives, for example $\Large \frac{\partial a^{(l)}_i}{\partial z^{(l)}_j}$, we mean its value a the point $z^{(l)}_j$, that is 
$$
\frac{\partial a^{(l)}_i}{\partial z^{(l)}_j} = 
\frac{\partial a^{(l)}_i}{\partial z^{(l)}_j} (z^{(l)}_j)
$$
# Gradients and Jacobian matrices notation and appearance
For more explanation about notation and appearance of gradients and Jacobian matrices used in this document, refer to the documents below:
- [[Jacobian matrix]]
- [[Gradient vector]]

When we calculate derivatives w.r.t. a matrix (for example $W$), we use vectorization $\text{vec}()$ as described here - [[Jacobian matrix - Input - matrix & output - vector]].
# Function dependencies and the chain rule
Before we go to calculating derivatives, let's check what dependencies between functions we have, so we know how to use the gradient chain rule ([[Chain rule|link]]).

It is also good to remind interpretations of:
- Derivative - [[Derivative|link]]
- Chain rule - [[Jacobian chain rule|link]]

We know, that:
$$
\large \begin{align}
& L = \mathcal{L}(a^{(L)}, y) \implies L \text{ depends on } a^{(L)} \\
& a^{(l)} = f_l(z^{(l)}) \implies a^{(l)} \text{ depends on } z^{(l)},\ \forall l \\
& z^{(l)} = W^{(l)} a^{(l - 1)} + b^{(l)} \implies 
z^{(l)} \text{ depends on } a^{(l - 1)}, W^{(l)}, b^{(l)},\ \forall l \\
\end{align}
$$
So that means, that the loss $L$ is the following composition of functions:
$$
\large
L = \mathcal{L} \circ f^{(L)} \circ z^{(L)} \circ f^{(L - 1)} \circ z^{(L - 1)} \circ \ldots \circ f^{(1)} \circ z^{(1)}
$$
so we have a chain of dependencies:
- $L$ depends on $a^{(L)}$
- $a^{(L)}$ depends on $z^{(L)}$ 
- $z^{(L)}$ depends on $a^{(L-1)}$
- $a^{(L-1)}$ depends on $z^{(L-1)}$ 
- and so on

That means, that $L$ doesn't depend only on $a^{(L)}$, but also on every value on which $a^{(L)}$ depends, that is $z^{(L)}, a^{(L-1)}, \ldots$

Also, $z^{(1)}$ doesn't depend on any other function because $z^{(1)} (a^{(0)}) = W^{(1)} a^{(0)} + b^{(1)}$ where $a^{(0)}$ is an input (known value).

Using those dependencies, we can calculate derivatives using the chain rule. For example, because $L$ depends on $z^{(l)}$ and $z^{(l)}$ depends on $a^{(l-1)}$, we have:
$$
\Large
\nabla_{a^{(l-1)}}L = J^T_{a^{(l-1)}}(z^{(l)}) \nabla_{z^{(l)}}L
$$
where each derivative tells us what is a dependency between a function and its argument. Whether increasing a value of the argument, increases or decreases a value of the function:
- $\large \nabla_{a^{(l-1)}}L$ - Represents dependency of $L$ on $a^{(l-1)}$ 
- $\large J^T_{a^{(l-1)}}(z^{(l)})$ - Represents dependency of $z^{(l)}$ on $a^{(l-1)}$ 
- $\large \nabla_{z^{(l)}}L$ - Represents dependency of $L$ on $z^{(l)}$ 

We will be using this reasoning a lot in this document.
# Elementwise activations
Notice, that if we have elementwise activations, that is $\Large \frac{\partial a^{(l)}_i}{\partial z^{(l)}_j} = 0$ if $i \neq j$, then Jacobian matrix is a diagonal matrix ([[Diagonal matrix|link]]):
$$
\large J_{z^{(l)}}(a^{(l)}) = 
\text{diag}\left( \frac{\partial a^{(l)}_i}{\partial z^{(l)}_i} \right)_{i=1}^{n_l}
\leftarrow \text{shape } (n_l, n_l)
$$
and product of matrices becomes an elementwise multiplication ([[Elementwise matrix multiplication|link]]):
$$
\large
J^T_{z^{(l)}}(a^{(l)}) \nabla_{a^{(l)}}L = 
\text{diag}\left( \frac{\partial a^{(l)}_i}{\partial z^{(l)}_i} \right)_{i=1}^{n_l}
\nabla_{a^{(l)}}L = 
\left( \frac{\partial a^{(l)}_i}{\partial z^{(l)}_i} \right)_{n_l \times 1}
\odot \nabla_{a^{(l)}} L
$$
where $\large \left( \frac{\partial a^{(l)}_i}{\partial z^{(l)}_i} \right)_{n_l \times 1}$ has shape $(n_l, 1)$.

We will use that later in this document.
# Delta
Let's denote as delta:
$$
\Large
\delta^{(l)} = \nabla_{z^{(l)}} L \leftarrow \text{shape } 
(n_l, 1)
$$
We will show later how to calculate recursively $\large \delta^{(l - 1)}$ using $\large \delta^{(l)}$.

Values $\large \delta^{(l)}$ will be used to calculate $\Large \nabla_{W^{(l)}} L$ and $\Large \nabla_{b^{(l)}} L$ for every layer $l$ .
# Last-layer pre-activation derivative (the starting point)
We start with calculating derivative of the loss w.r.t pre-activation from the last layer $z^{(L)}$.

As mentioned earlier in the section about function dependencies, $L$ depends on $a^{(L)}$ and $a^{(L)}$ depends on $z^{(L)}$ and because of that, using the chain rule, we have:
$$
\Large
\delta^{(L)} = \nabla_{z^{(L)}}L = J^T_{z^{(L)}}(a^{(L)}) \nabla_{a^{(L)}}L
\leftarrow \text{shape } (n_L, 1)
$$
If we have elementwise activations, then product of matrices becomes elementwise multiplication as explained earlier:
$$
\Large \delta^{(L)} = 
\left( \frac{\partial a^{(L)}_i}{\partial z^{(L)}_i} \right)_{n_L \times 1}
\odot \nabla_{a^{(L)}} L

$$
where both $\large \left( \frac{\partial a^{(L)}_i}{\partial z^{(L)}_i} \right)_{n_L \times 1}$ and $\large \nabla_{a^{(L)}} L$ has shape $(n_L, 1)$.

We can calculate $\Large \frac{\partial a^{(L)}_i}{\partial z^{(L)}_j} (z^{(L)}_j)$ values, since:
- We know the values of $z^{(L)}_j$ (that's the output for a given data input $a^{(0)}$) 
- $a^{(L)}_i$ depends directly on $z^{(L)}_j$ so there is no need for using the chain rule

Similarly, we can calculate $\large \nabla_{a^{(L)}} L$ since we know the value of $a^{(L)}$ and $L$ depends on $a^{(L)}$ directly.
# Derivative of $z^{(l)}$ w.r.t. $W^{(l)}$ 
We know, that equation for $z^{(l)}$ is:
$$
\large
z^{(l)} = W^{(l)} a^{(l - 1)} + b^{(l)}
$$
So, after differentiating both sides w.r.t. the vectorized matrix $W^{(l)}$ ([[Vectorization of a matrix|link]]), we get:
$$
\large
\frac{\partial z^{(l)}} {\partial \text{vec}(W^{(l)})} =
\frac{\partial (W^{(l)} a^{(l - 1)})} {\partial \text{vec}(W^{(l)})}
$$
We use vectorized matrix $W^{(l)}$ because $z^{(l)}$ is a vector and we want the Jacobian $\large \frac{\partial z^{(l)}} {\partial \text{vec}(W^{(l)})}$ to be a matrix as explained here - [[Jacobian matrix - Input - matrix & output - vector|link]].

Using the fact, that ([[vec–Kronecker derivative identity|link]]):
$$
\frac{\partial (Wa)} {\partial \text{vec}(W)} = a^T \otimes I_{n_l}
$$
we have:
$$
\large
J_{\text{vec}(W^{(l)})} (z^{(l)}) = 
\frac{\partial z^{(l)}} {\partial \text{vec}(W^{(l)})} = a^{(l-1)T} \otimes I_{n_l}
\text{ - shape } (n_l, n_l n_{l-1})
$$
where:
- $\large I_{n_l}$ is an identity matrix ([[Identity matrix|link]]) of shape $(n_l, n_l)$ 
- $\large a^{(l-1)T}$ has shape $(1, n_{l-1})$ 
- $\otimes$ is the Kronecker product ([[Kronecker product|link]])
# Gradients w.r.t. weights and biases
## Biases
Since the formula for $z^{(l)}$ is:
$$
\large
z^{(l)} = W^{(l)} a^{(l - 1)} + b^{(l)}
$$
Derivative for $z^{(l)}$ w.r.t. to the bias is an identity matrix:
$$
\large \text{1) }
J_{b^{(l)}} (z^{(l)}) = \frac{\partial z^{(l)}} {\partial b^{(l)}} = I_{n_l}
$$
As mentioned earlier in the section about function dependencies, $L$ depends on $z^{(l)}$ and $z^{(l)}$ depends on $b^{(l)}$ and because of that, using the chain rule, we have:
$$
\Large
\nabla_{b^{(l)}}L = J^T_{b^{(l)}}(z^{(l)}) \nabla_{z^{(l)}}L
$$
Using the value $\large J_{b^{(l)}} (z^{(l)})$ from the equation 1 which we just calculated, we have:
$$
\Large
\nabla_{b^{(l)}}L = I_{n_l} \cdot \nabla_{z^{(l)}}L =
\delta^{(l)} \leftarrow \text{ shape } (n_l, 1)
$$
## Weights
As mentioned earlier in the section about function dependencies, $L$ depends on $z^{(l)}$ and $z^{(l)}$ depends on $W^{(l)}$ and because of that, using the gradient chain rule, we have:
$$
\Large
\nabla_{\text{vec}(W^{(l)})}L = J^T_{\text{vec}(W^{(l)})}(z^{(l)}) \nabla_{z^{(l)}}L
$$
where we vectorize $W^{(l)}$ because we want:
- Both values $\large \nabla_{\text{vec}(W^{(l)})}L$ and $\large \nabla_{z^{(l)}}L$ to be gradients ($\large \nabla_{(W^{(l)})}L$ would be a Jacobian matrix)
- $\large J^T_{\text{vec}(W^{(l)})}(z^{(l)})$ to be a Jacobian matrix as explained here - [[Jacobian matrix - Input - matrix & output - vector|link]].

Using previously calculated $\large J_{\text{vec}(W^{(l)})}(z^{(l)})$ and definition of $\delta^{(l)}$, we get:
$$
\large
\nabla_{\text{vec}(W^{(l)})}L = 
\left( a^{(l-1)T} \otimes I_{n_l} \right)^T \delta^{(l)}
$$
Using the fact, that ([[Transposed Kronecker product|link]]):
$$
(A \otimes B)^T = A^T \otimes B^T
$$
We have:
$$
\large
\nabla_{\text{vec}(W^{(l)})}L = \left( a^{(l-1)} \otimes I_{n_l} \right) \delta^{(l)}
$$
Using the fact, that ([[Matrix vectorization identity|link]]):
$$
\text{vec}(AXB^T) = (B \otimes A)\text{vec}(X)
$$
and putting:
- $B = a^{(l-1)}$ 
- $A = I_{n_l}$ 
- $\text{vec}(X) = X = \delta^{(l)}$ - because $\delta^{(l)}$ is already a column vector, so $\delta^{(l)} = \text{vec}(\delta^{(l)})$ 

we have:
$$
\large
\nabla_{\text{vec}(W^{(l)})}L = \text{vec}(\delta^{(l)} (a^{(l-1)T}))
$$
If we un-vectorize both sides, we get formula for Jacobian (as explained here - [[Un-vectorizing gradient to obtain Jacobian matrix|link]]):
$$
\large J_{W^{(l)}}(L) = \delta^{(l)} (a^{(l-1)})^T 
\leftarrow \text{ shape } (n_l, n_{l-1})
$$
# Backpropagate the error to previous layers
Now we will show how to calculate $\large \delta^{(l - 1)}$ using $\large \delta^{(l)}$.

From the definition:
$$
\large \text{1) } \delta^{(l - 1)} = \Large \nabla_{z^{(l-1)}} L
$$
As mentioned earlier in the section about function dependencies, $L$ depends on $a^{(l-1)}$ and $a^{(l-1)}$ depends on $z^{(l-1)}$, and because of that, using the chain rule, we have:
$$
\large \text{2) } \nabla_{z^{(l-1)}}L = J^T_{z^{(l-1)}}(a^{(l-1)}) \nabla_{a^{(l-1)}}L
$$
So using the equation 2 for the equation 1 we get:
$$
\large \text{1.1) }
\delta^{(l - 1)} = J^T_{z^{(l-1)}}(a^{(l-1)}) \nabla_{a^{(l-1)}}L
$$


Similarly, using the fact that $L$ depends on $z^{(l)}$ and $z^{(l)}$ depends on $a^{(l-1)}$, we get:
$$
\Large \text{3) }
\nabla_{a^{(l-1)}}L = J^T_{a^{(l-1)}}(z^{(l)}) \nabla_{z^{(l)}}L
$$
Since $\large z^{(l)} = W^{(l)} a^{(l - 1)} + b^{(l)}$, we have:
$$
\Large
J_{a^{(l-1)}}(z^{(l)}) = W^{(l)}
$$
So the equation 3 becomes:
$$
\Large \text{3.1) }
\nabla_{a^{(l-1)}}L = (W^{(l)})^T \delta^{(l)}
$$


Using the equation 3.1 for the equation 1.1, results in:
$$
\Large \text{1.2) }
\delta^{(l-1)} = J^T_{z^{(l-1)}}(a^{(l-1)}) (W^{(l)})^T \delta^{(l)}
$$

If activations $a^{(l-1)}$ are elementwise, that becomes elementwise multiplication, as explained earlier in the section about elementwise activations:
$$
\large
\delta^{(l-1)} =
\left( \frac{\partial a^{(l-1)}_i} {\partial z^{(l-1)}_i} \right)_{n_{l-1} \times 1}
\odot (W^{(l)})^T \delta^{(l)}
$$
where $\large \left( \frac{\partial a^{(l-1)}_i}{\partial z^{(l-1)}_i} \right)_{n_{l-1} \times 1}$ and $\large (W^{(l)})^T \delta^{(l)}$ have shape $(n_{l-1}, 1)$.

We can calculate $\Large \frac{\partial a^{(l-1)}_i}{\partial z^{(l-1)}_j} (z^{(l-1)}_j)$ values, since:
- We know the values of $z^{(l-1)}_j$ (that's the output for a given data input $a^{(0)}$)
- $a^{(l-1)}_i$ depends directly on $z^{(l-1)}_j$ 
# Summary
Formulas for derivative of loss w.r.t to weights and biases are:
$$
\large J_{W^{(l)}}(L) = \delta^{(l)} (a^{(l-1)})^T 
\leftarrow \text{ shape } (n_l, n_{l-1})
$$
$$
\large \nabla_{b^{(l)}}L = \delta^{(l)} \leftarrow \text{ shape } (n_l, 1)
$$
And to calculate needed values $\large \delta^{(l)}$, we start with calculating delta for the last layer $L$ :
$$
\Large \delta^{(L)} =
\nabla_{z^{(L)}}L = J^T_{z^{(L)}}(a^{(L)}) \nabla_{a^{(L)}}L
$$
which for elementwise activations can be written using elementwise multiplication:
$$
\Large
\delta^{(L)} = 
\left( \frac{\partial a^{(L)}_i}{\partial z^{(L)}_i} \right)_{n_L \times 1}
\odot \nabla_{a^{(L)}} L
$$
and then, we use a recursive formula to calculate deltas for other layers $l$ :
$$
\Large
\delta^{(l-1)} = J^T_{z^{(l-1)}}(a^{(l-1)}) (W^{(l)})^T \delta^{(l)}
$$
which for elementwise activations can be written using elementwise multiplication:
$$
\large
\delta^{(l-1)} =
\left( \frac{\partial a^{(l-1)}_i} {\partial z^{(l-1)}_i} \right)_{n_{l-1} \times 1}
\odot (W^{(l)})^T \delta^{(l)}
$$
# Why backpropagation is effective
We could calculate every value $\delta^{(l)}$ using this formula:
$$
\Large
\delta^{(l)} = \nabla_{z^{(l)}}L = J^T_{z^{(l)}}(a^{(l)}) \nabla_{a^{(l)}}L
$$
because we know values of $z^{(l)}$ and $a^{(l)}$.

But we can't calculate $\large \nabla_{a^{(l)}}L$ directly, since $L$ doesn't depend on $a^{(l)}$ directly. We would need to use the chain rule of the entire chain of dependencies:
$$
L = a^{(L)} \circ z^{(L)} \circ a^{(l-1)} \dots \circ z^{(l+1)} \circ a^{(l)}
$$
so we would need to calculate it this way:
$$
\Large
\nabla_{a^{(l)}}L = J^T_{a^{(l)}}(z^{(l+1)}) J^T_{z^{(l+1)}}(a^{(l+1)}) \dots J^T_{z^{(L)}}(a^{(L)}) \nabla_{a^{(L)}}L
$$
If we do this for calculating $\delta^{(l)}$ for every $l$, we would perform huge amount of calculations.

But if we use this formula instead:
$$
\Large
\delta^{(l-1)} = J^T_{z^{(l-1)}}(a^{(l-1)}) (W^{(l)})^T \delta^{(l)}
$$
then:
- We are reusing $\delta^{(l)}$ to calculate the next value $\delta^{(l-1)}$ 
- We can calculate directly $\large J^T_{z^{(l-1)}}(a^{(l-1)})$ without using the chain rule, since $a^{(l-1)}$ depends directly on $z^{(l-1)}$ 
thanks to which we are saving a lot of effort (much less calculations to do).

#MachineLearning 