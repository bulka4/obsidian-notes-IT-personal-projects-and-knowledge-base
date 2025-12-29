Tags: [[__Machine_Learning]]

# Introduction
When training a statistical model, it is often used to define a probability distribution function of random variables which generated our given dataset.

We want that function to be as close as possible to the true probability distribution function of those random variables.

That's why we sometimes train models in such a way, as to minimize the divergence (difference) between those two probability distribution functions (the modeled one and the true one).

We do this by using such a loss function, that minimizing that loss function is equivalent to minimizing the divergence.
# Calculating a divergence
In order to calculate a divergence between two probability distributions, we can use for example:
- KL Divergence - [[KL Divergence|link]]
- 

#MachineLearning 