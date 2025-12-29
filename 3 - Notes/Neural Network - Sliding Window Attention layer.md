Tags: [[__Machine_Learning]]

# Introduction
In a standard attention layer ([[Neural Network - Attention layer|link]]), for every input token $\large x_i$ , we calculate scores:
$$
\large 
\text{score}_{ij} = Q_i K_j^T
$$
between that token and every other input token $\large x_j,\ j = 1, \ldots, T$ which reflects a relation between those input tokens (how much token $x_i$ attends to other tokens $x_j$).

In a sliding window attention, for every input token $\large x_i$ , we only calculate scores between that token and tokens $\large x_j,\ j \in [i - w, i + w]$ , where $w$ is a chosen number, so called window size.

So for every input token $x_i$ , we check its relation only to neighboring tokens.

It is useful when input sequence is very long and we want to save computational power.

#MachineLearning 