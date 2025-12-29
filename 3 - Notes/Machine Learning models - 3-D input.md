Tags: [[__Machine_Learning]]

# Introduction
When input for a machine learning model is a 3-D tensor, that can be viewed as a matrix where each element is a vector.

We usually denote its shape as $(H, W, C)$ which indicates:
- $H$ - Input height
- $W$ - Input weight
- $C$ - Number of channels
# Examples
## Image
For example, such an input might be an image where shape indicates image size in pixels image and values are vectors indicating a color of that pixel (for example RGB uses a set of 3 numbers to encode a color).

So a 3-D tensor of shape $(100, 100, 3)$ would be a picture of a size $100 \times 100$ pixels and it uses RGB (set of 3 numbers) to encode pixels' colors.
## Time series
Or it can be a time series data, where:
- $H$ indicates a sequence length (number of timesteps) 
- $W$ indicates how many numbers we have for one timestep
- $C = 1$ - A single channel

Representing a time series data sample of shape $(H, W, 1)$ is the same as representing it as a 2-D tensor of shape $(H, W)$. Adding additional dimension indicating a single channer $C = 1$, doesn't change anything but sometimes we need to have a 3-D input to use some of the programming frameworks.

For more information about interpretation and examples of such a dataset, refer to this document - [[Machine Learning models - 2-D input|link]].

#MachineLearning 