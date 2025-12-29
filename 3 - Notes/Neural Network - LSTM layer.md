Tags: [[__Machine_Learning]]

# Introduction
LSTM (Long short term memory) layer is a type of a recurrent neural network layer designed to deal effectively with the problem with vanishing and exploding gradients as described here - [[Neural Network - Recurrent layer]] in the section about problems.

Before we learn about the LSTM layer, we should become familiar with concepts described in the mentioned document about a recurrent layer.

LSTM uses a memory cell and gates to control what information is kept, forgotten, or output at each timestep.
# How it works
At each timestep $t$, LSTM generates, like in the standard recurrent:
- Hidden state $\large h_t \in \mathbb{R}^m$ - Like in the standard recurrent layer
- Additional output $\large y_t = g(h_t) \in \mathbb{R}^n$ 

And additionally:
- Cell state $\large c_t \in \mathbb{R}^m$ - The memory that carries information across timesteps

It uses three gates and one candidate value to update these states:

| Gate                           | Purpose                                            | Formula                                                    |
| ------------------------------ | -------------------------------------------------- | ---------------------------------------------------------- |
| Forget gate $\large f_t$       | Decide what to forget from $c_{t-1}$               | $\large f_t = \sigma (W_f x_t + U_f h_{t-1} + b_f)$        |
| Input gate $\large i_t$        | Decide what new info to add                        | $\large i_t = \sigma (W_i x_t + U_i h_{t-1} + b_i)$        |
| Candidate $\large \tilde{c_t}$ | Proposed new memory (new value for the cell state) | $\large \tilde{c_t} = \tanh (W_c x_t + U_c h_{t-1} + b_c)$ |
| Output gate $\large o_t$       | Decide what to output as a hidden state            | $\large o_t = \sigma (W_o x_t + U_o h_{t-1} + b_o)$        |
And we have the following shapes:
$$
\large \begin{align}
& f_t, i_t, \tilde{c_t}, o_t \in \mathbb{R}^m \\
& x_t \in \mathbb{R}^d \\
& W_f, W_i, W_c, W_o \in \mathbb{R}^{m \times d} \\
& U_f, U_i, U_c, U_o \in \mathbb{R}^{m \times m} \\
& b_f, b_i, b_c, b_o \in \mathbb{R}^{m} \\
\end{align}
$$

We update the cell state $c_t$ and hidden state $h_t$ using the following formula:
$$
\large \begin{align}
& c_t = f_t \odot c_{t-1} + i_t \odot \tilde{c_t} \\
& h_t = o_t \odot \tanh(c_t)
\end{align}
$$
where:
- $\odot$ - Elementwise multiplication ([[Elementwise matrix multiplication|link]])
# Single vectorized equation
The entire operation of a LSTM layer can be written in a single, vectorized equation:
$$
\begin{pmatrix}
f_t \\
i_t \\
o_t \\
\tilde{c_t}
\end{pmatrix}
= \begin{pmatrix}
\sigma \\
\sigma \\
\sigma \\
\tanh
\end{pmatrix}
(W x_t + U h_{t-1} + b)
$$
where:
$$
W = \begin{pmatrix}
W_f \\
W_i \\
W_c \\
W_o
\end{pmatrix} \in \mathbb{R}^{4m \times d}
, \quad U = \begin{pmatrix}
U_f \\
U_i \\
U_c \\
U_o
\end{pmatrix} \in \mathbb{R}^{4m \times m}
, \quad b= \begin{pmatrix}
b_f \\
b_i \\
b_c \\
b_o
\end{pmatrix} \in \mathbb{R}^{4m}
$$
# How LSTM helps with the vanishing / exploding gradient problem
Like described here - [[Neural Network - Recurrent layer]], recurrent layer has a problem with vanishing / exploding gradients.

In LSTM that's not a problem, because in order to use optimization algorithm like gradient descent ([[Gradient Descent - ML|link]]), we need to calculate derivatives of $c_t$, for which Jacobian matrix ([[Jacobian matrix|link]]) is:
$$
\large
J_{c_t}(c_{t-1}) = \text{diag}(f_t^{(k)})_1^m = \text{diag}(f_t)
$$
where:
- $f_t = (f_t^{(k)})_{m \times 1}$ is a column vector (one column matrix)
- $\text{diag}(f_t^{(k)})_1^m = \text{diag}(f_t)$ is a diagonal matrix with values $f_t^{(k)}$ on the diagonal ([[Diagonal matrix|link]]). 

That's because:
$$
\large
\frac{\partial c_t^{(k)}}{\partial c_{t-1}^{(j)}} = \begin{cases}
f_t^{(k)} & j=k \\
0 & j \neq k
\end{cases}
$$
When LSTM layer's output is $y_T$, then loss function is:
$$
L = \mathcal{L}(y_T)
$$
In order to reduce loss using an optimization algorithm, like gradient descent ([[Gradient Descent - ML|link]]), we need gradients of that loss. Using the gradient chain rule ([[Chain rule|link]]), we have:
$$
\large
\nabla_{c_1}L = \prod_{i=2}^T J^T_{c_{i-1}}(c_i) J^T_{c_T}(y_T) \nabla_{y_T}L
$$
Using previously shown formula for $\large J_{c_t}(c_{t-1})$, that equation changes into:
$$
\large
\nabla_{c_1}L = \prod_{i=2}^T \text{diag}(f_i) J^T_{c_T}(y_T) \nabla_{y_T}L
$$
what can be also written as:
$$
\large
\nabla_{c_1}L = (f_2 \odot \dots \odot f_T) J^T_{c_T}(y_T) \nabla_{y_T}L
$$
where $\odot$ is elementwise multiplication ([[Elementwise matrix multiplication|link]]).

That solves vanishing / exploding gradient problem, if values of each $\large f_i$ are close to 1.

#MachineLearning 