Tags: [[_DeepSpeed]], [[__Machine_Learning_Engineering]]

# Introduction
When working with transformers ([[Transformer model|link]]) in DeepSpeed for token generation ([[Token generation|link]]) and our input sequence is very long, sometimes it is worth to use sliding window attention ([[Neural Network - Sliding Window Attention layer|link]]) in order to save computational power.

Instead of calculating scores between an input token $x_i$ and every other input token $\large x_j,\ j = 1, \ldots, T$ :
$$
\large 
\text{score}_{ij} = Q_i K_j^T
$$

We do this only for tokens neighboring with $x_i$ , that is $\large x_j,\ j \in [i - w, i + w]$ , where $w$ is a chosen number called window size.

#DeepSpeed #MLEngineering 