Tags: [[__Machine_Learning]]

# Introduction
When input for a machine learning model is a 2-D tensor, that is a matrix, we usually denote its shape as $(H, W)$ which indicates:
- $H$ - Input height
- $W$ - Input weight

2-D tensor of shape $(H, W)$ can be also represented as a 3-D tensor of shape $(H, W, 1)$ .
# Examples
## Image
For example, such an input might be an image where shape indicates image size in pixels and values indicates a color of that pixel.

So 2-D input of shape $(100, 100)$ would be a picture of a size $100 \times 100$ pixels.
## Time series
Or it can be a time series data, where:
- $H$ indicates a sequence length (number of timesteps) 
- $W$ indicates how many numbers (features) we have for one timestep
### Sensors measurements
For example such a time series data can be measurements from multiple sensors, which measures for example heat, speed and pressure, and each data sample contains a series of 1000 measurements made on a car engine during driving.

In that case, $H$ is a number of measurements in a single data sample (1000) and $W$ is a number of sensors (3).

#MachineLearning 