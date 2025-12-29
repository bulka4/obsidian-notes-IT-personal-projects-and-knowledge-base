Tags: [[__Machine_Learning]]

# Introduction
We can do the following:
- Use a convolution layer ([[Neural Network - Convolution layer|link]]) to generate set of features maps which combined have shape $(H, W, C)$
	- It can be seen as a matrix where each element is a vector of length $C$ 
	- $C$ is a number of filters applied
- Flatten that set of features maps into a matrix of shape $(H \cdot W, C)$ 
- Use it as an input for an attention layer. So we are going to have $H \cdot W$ input tokens, each of length $C$ 

#MachineLearning 