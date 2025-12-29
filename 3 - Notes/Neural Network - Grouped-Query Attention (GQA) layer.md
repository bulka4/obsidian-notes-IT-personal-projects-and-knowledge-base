Tags: [[__Machine_Learning]]

# Introduction
Grouped-Query Attention (GQA) neural network layer is a simplified version of a multi-head attention (MHA) ([[Neural Network - Multi-Head Attention (MHA) layer|link]]).

In MHA, we have separate matrices $Q_h, K_h, V_h$ per each head $h$, while in MQA we have only separate Query matrices per head $Q_h$ , while number of matrices $K, V$ is reduced.

We group Query matrices:
$$
\Large \begin{align}
& \text{group 1} = Q_{I_1} = \{ Q_i : i \in I_1 \} \\
& \dots \\
& \text{group n} = Q_{I_n} = \{ Q_i : i \in I_n \} \\
\end{align}
$$
And for every group $\Large Q_{I_i}$ of Query matrices, we create one, separate pair of Key-Value matrices $K_i$ and $V_i$.

Thanks to this, we have much less computations to do but performance might be slightly worse.

It is a middle ground between MHA and MQA (multi-query attention) ([[DeepSpeed - MQA and GQA|link]]), in this method we have less matrices than in MHA but more than in MQA.

#MachineLearning 