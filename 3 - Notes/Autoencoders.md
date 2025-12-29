Tags: [[__Machine_Learning]]

# Introduction
Autoencoders are a type of neural network ([[Neural Network|link]]) designed to learn efficient representations of data. They take an input $x$, produce an output $y$, and tries to reconstruct the original input $x$.

Output $y$ can be interpreted as a new version of features $x$ ([[Dataset of observations of random variables X, Y - Variables per sample, feature and target variable|link]]). It is often used in anomaly detection ([[Anomaly Detection models|link]]), dimensionality reduction ([[Dimensionality reduction|link]]) or data compression.
# Encoder
Encoder compresses the input into a lower-dimensional representation. It learns the 'essence' of that input, extracts the most important information.
$$
y = \text{Encoder}(x)
$$
Output $y$ is called a latent vector.
# Decoder
Decoder reconstructs the original input using generated latent vector $y$ :
$$
\hat{x} = \text{Decoder}(y)
$$
We want $\hat{x}$ to be as similar as possible to the original $x$.
# Training Autoencoder - Reconstruction loss
To train an autoencoder, we use a loss function and we consider $x$ as the true value and $\hat{x}$ as the prediction.
# Autoencoders use cases
- Anomaly detection - [[Autoencoders - Anomaly detection|link]]
- Dimensionality reduction - [[Autoencoders - Dimensionality reduction|link]]

#MachineLearning 