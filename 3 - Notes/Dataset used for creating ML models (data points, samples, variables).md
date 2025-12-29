Tags: [[__Machine_Learning]]

# Introduction
In order to create a machine learning model, we need a dataset which is a collection of objects.
# Dataset definition
As a dataset, we define a set $D$ :
$$
\large
D = \{x_1, \dots, x_n\} = \{x_i\}_{i=1}^n \subseteq \mathcal{X}
$$
where $\large (\mathcal{X}, \mathcal{B}_{\mathcal{X}})$ is a measurable space ([[Measure space|link]]).
# Data points / samples
Each element $x_i$ of a dataset $D$ is called a data point / data sample. Each data point can be multi-dimensional tuple ([[Tuple|link]]):
$$
\large
x_i = (x_{i1}, \dots, x_{im}) \in \mathcal{X} = \prod_{j=1}^m \mathcal{X}_j
$$
# Variables
Each component $x_{ij}$ is called a variable and it belongs to its own domain:
$$
x_{ij} \in \mathcal{X}_j
$$
So the full space of the entire dataset is a product space ([[Product measurable space|link]]):
$$
\large
\mathcal{X} = \prod_{j=1}^m \mathcal{X}_j, \quad
\mathcal{B}_{\mathcal{X}} = \bigotimes_{j=1}^m \mathcal{B}_{\mathcal{X}_j}
$$
# Features and target variables
Components $x_{ij}$ of a data point $x_i$ can be grouped into features and target variables as described here - [[Features and target variables]].
# Variable types
Each component $x_{ij}$ is called a variable and there are different types described here - [[Types of variables used for creating ML models|link]].
# Examples
## House prices
We might have a dataset with houses features and prices, and model can try to predict the prices:
- Features:
	- $x_1 \in \mathbb{R}$ - Area
	- $x_2 \in \mathbb{N}$ - Number of bedrooms
	- $x_3 \in \{0, 1\}$ - Whether it has a garden
- Target variable:
	- $x_4 \in \mathbb{R}$ - Price of the house
## Image classification
A dataset can consist of classified images. 

Each image is represented as a 3-D tensor ([[Tensor|link]]) of shape $(H, W, 3)$, where:
- $H$ - Image height in pixels
- $W$ - Image width in pixels
- Color of each pixel is encoded using a set of 3 numbers (RGB)

So it can be seen as a matrix $A$ of shape $(H, W)$ where each element $a_{ij}$ is a set of 3 numbers representing a color of the pixel from the $i$-th row and $j$-th column (pixel at height $i$ and width $j$ in the image).

So in that case, our dataset consist of:
- Features:
	- $x_1 \in \mathbb{R}^{H \times W \times 3}$ - Image
- Target variable:
	- $x_2 \in \{ \text{cat}, \text{dog} \}$ - Class of the image, what that image shows
## Text classification
Another example is a dataset with classified sentences, for example comments classified as positive or negative.

In that case, we have:
- Features:
	- $x_i = (w_{i1}, \dots, w_{iT}) \in A^T$ - A sentence:
		- That is a sequence (tuple ([[Tuple|link]])) of $T$ words
		- $A = \{\text{word 1}, \dots, \text{word n}\}$ is a set of all the possible words
		- If sentence is shorter than $T$ words, then missing words are some established 'empty' words called padding tokens
- Target variable:
	- $x_2 \in \{ \text{positive}, \text{negative} \}$ - Class of the sentence

#MachineLearning 