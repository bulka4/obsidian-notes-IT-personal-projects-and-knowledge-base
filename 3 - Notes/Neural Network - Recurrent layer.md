Tags: [[__Machine_Learning]]

# Introduction
Recurrent Neural Network is a model that can be used for both classification and regression.

It is primarily used when we take a sequential data as an input, e.g. time series or text.

In a sequential data, it takes as an input value from each timestep one by one and also output from the previous timestep.
# Types of recurrent layers
Below are listed multiple types of a recurrent layers with links to materials, from which we can learn more about them:
- Standard one (described in this document)
- LSTM - [[Neural Network - LSTM layer]]
- GRU - [[Neural Network - GRU layer]]
# Data input
Input for a recurrent layer is a sequence of vectors, i.e. a 2-D tensor of shape $(T, d)$ (can be viewed as a matrix):
$$
X = (x_1, \ldots, x_T), \quad x_i \in \mathbb{R}^d, \quad X \in \mathbb{R}^{T \times d}
$$
where each value $x_i$ is processed separately, one by one.
# Generating hidden states and outputs
Recurrent layer works recursively. 

At the step $t$, it generates:
- A **hidden state** $\large h_t \in \mathbb{R}^m$ 
- An **additional output** $\large y_t \in \mathbb{R}^n$ 

It is done in the following way:
- Take as an input value $x_t$ and hidden state $h_{t-1}$ 
- Produce two outputs:
	- New hidden state $h_t$ 
	- Additional output $y_t$ 

Each hidden state $h_t$ and output $y_t$ are created using the following formulas:
$$
\large
\begin{align}
& f(h_{t-1}, x_t) = W_x x_t + W_h h_{t-1} + b \\
& h_t = \sigma(f(h_{t-1}, x_t)) =  \sigma(W_x x_t + W_h h_{t-1} + b) \\
& y_t = g(h_t)
\end{align}
$$
where:
- $\large W_x \in \mathbb{R}^{m \times d}$ - Weights for the input $x_t$ (the same for every input)
- $\large W_h \in \mathbb{R}^{m \times m}$ - Weights for the previous hidden state $h_{t-1}$ (the same for every hidden state)
- $b \in \mathbb{R}^m$ - Bias
- $\sigma$ - Activation function
- $h_0$ is fixed (might be a learnable parameter)
## Visualization
Here we have visualized how recurrent layer performs calculations:
![[recurrent layer calculations.png]]
## Final output
The final output of a recurrent layer is one of the options:
- $h_T$ or $y_T$ - For example for classification of the entire sequence
- $(y_1, \ldots, y_T)$ or $(h_1, \ldots, h_T)$ - For example, those numbers can represent:
	- Words for a translation of the input sentence
	- Input for another recurrent layer
## Recurrent layer as a function composition
Values $y_T$ and $h_T$ are the following compositions of functions:
$$
\large
\begin{align}
& y_T = \underbrace{g \circ f \circ \sigma \circ f \circ \sigma \circ \dots\circ f \circ \sigma}_{
(2T + 1) \text{ functions in total}} \\
& h_T = \underbrace{f \circ \sigma \circ f \circ \sigma \circ \dots\circ f \circ \sigma}_{
2T \text{ functions in total}} \\
\end{align}
$$
# Stacked recurrent layers
We can use an output from one recurrent layer:
$$
(y_1, \ldots, y_T) \text{ or } (h_1, \ldots, h_T)
$$
as an input for another one.
# Recurrent layer problems
## Vanishing / exploding gradients
If we want to train a model which uses a recurrent layer, we need to use optimization algorithm, like gradient descent, which uses gradients of a loss function to update model's parameters.

Like described here - [[Gradient Descent - ML]], when gradients of a loss are very big or very small, optimization algorithm doesn't work well.

When we have a loss function which depends on $h_T$ (layer's output):
$$
L = \mathcal{L}(h_T)
$$
then in order to calculate its gradient w.r.t. $h_1$, using the gradient chain rule ([[Chain rule|link]]), we use the formula:
$$
\large
\nabla_{h_1}L = \prod_{i=2}^T J^T_{h_{i-1}}(h_i) \nabla_{h_T}L
$$
or similarly, when layer's output is $y_T$ and loss function is  $L = \mathcal{L}(y_T)$ :
$$
\large
\nabla_{h_1}L = \prod_{i=2}^T J^T_{h_{i-1}}(h_i) J^T_{h_T}(y_T)
\nabla_{y_T}L
$$
where:
- $\large \nabla_{h_1}L$ - gradient ([[Gradient vector|link]])
- $\large J^T_{h_{i-1}}(h_i)$ - Transposed Jacobian matrix ([[Jacobian matrix|link]])

If values in every $\large J^T_{h_{i-1}}(h_i)$ are smaller than 1, then we have vanishing gradient problem ($\large \nabla_{h_1}L$ will be very small).

If values in every $\large J^T_{h_{i-1}}(h_i)$ are bigger than 1, then we have exploding gradient problem ($\large \nabla_{h_1}L$ will be very big).
# Useful links
- RNN:
	- [https://github.com/Site1997/RNN-implementation](https://github.com/Site1997/RNN-implementation)
	- [https://medium.com/@jianqiangma/all-about-recurrent-neural-networks-9e5ae2936f6e](https://medium.com/@jianqiangma/all-about-recurrent-neural-networks-9e5ae2936f6e
	- [https://www.analyticsvidhya.com/blog/2019/01/fundamentals-deep-learning-recurrent-neural-networks-scratch-python/](https://www.analyticsvidhya.com/blog/2019/01/fundamentals-deep-learning-recurrent-neural-networks-scratch-python/)
	- [https://www.youtube.com/watch?v=AsNTP8Kwu80](https://www.youtube.com/watch?v=AsNTP8Kwu80)
	- [https://www.youtube.com/watch?v=YCzL96nL7j0](https://www.youtube.com/watch?v=YCzL96nL7j0) 
- LSTM
	- [https://colah.github.io/posts/2015-08-Understanding-LSTMs/](https://colah.github.io/posts/2015-08-Understanding-LSTMs/)

#MachineLearning 