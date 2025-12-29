Tags: [[__Machine_Learning]]

# Introduction
GRU (Gated Recurrent Unit) layer is a type of a recurrent neural network layer designed to deal effectively with the problem with vanishing and exploding gradients as described here - [[Neural Network - Recurrent layer]] in the section about problems.

To learn more about GRU, like how it helps with the vanishing / exploding gradient problem, refer to the document about LSTM - [[Neural Network - LSTM layer]]. 

Understanding LSTM will cause that we understand GRU, as they are very similar. GRU is simplified version of LSTM.
# How it works
At each timestep $t$, GRU generates, like in the standard recurrent layer:
- Hidden state $\large h_t \in \mathbb{R}^m$ 
- Additional output $\large y_t = g(h_t) \in \mathbb{R}^n$ 

It uses three gates and one candidate value to update these states:

| Gate                           | Purpose                                                              | Formula                                                    |
| ------------------------------ | -------------------------------------------------------------------- | ---------------------------------------------------------- |
| Update gate $\large z_t$       | Controls how much information from the previous hidden state to keep | $\large z_t = \sigma (W_z x_t + U_z h_{t-1} + b_z)$        |
| Rest gate $\large r_t$         | Controls how much of the past information to forget                  | $\large r_t = \sigma (W_r x_t + U_r h_{t-1} + b_r)$        |
| Candidate $\large \tilde{h_t}$ | Proposed new memory (new value for the hidden state)                 | $\large \tilde{h_t} = \tanh (W_h x_t + U_h h_{t-1} + b_h)$ |
And we have the following shapes:
$$
\large \begin{align}
& z_t, r_t, \tilde{h_t} \in \mathbb{R}^m \\
& x_t \in \mathbb{R}^d \\
& W_z, W_r, W_h \in \mathbb{R}^{m \times d} \\
& U_z, U_r, U_h \in \mathbb{R}^{m \times m} \\
& b_z, b_r, b_h \in \mathbb{R}^{m} \\
\end{align}
$$

Hidden state $h_t$ is updated using the formula:
$$
\large
h_t = (1 - z_t) \odot h_{t-1} + z_t \odot \tilde{h_t}
$$
Interpretation:
- If $z_t$ is close to zero, then we keep most of the old information (from the previous hidden state)
- If $z_t$ is close to one, then we erase most of the old information (from the previous hidden state) and we add a new information (from $\tilde{h_t}$)
# Key differences between GRU and LSTM
- There is no cell state $\large c_t$ in GRU
- In LSTM there are 3 gates (forget, input, output) and in GRU there are two (reset, update)
- So LSTM is in general more complex, takes more time to train, but performs better in complex tasks

#MachineLearning 