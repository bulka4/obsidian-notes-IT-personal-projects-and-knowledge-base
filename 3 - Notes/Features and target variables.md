Tags: [[__Machine_Learning]]

# Introduction
As described here - [[Dataset used for creating ML models (data points, samples, variables)|link]], for creating machine learning models, we use a dataset consisting of data samples:
$$
\large \begin{align}
& D = \{x_1, \dots, x_n\} \\
& x_i = (x_{i1}, \dots, x_{im}) \text{ - data sample}
\end{align}
$$
and each component $x_{ij}$ is called a variable.

In context of ML, we divide those variables into two groups:
- **Features** - Variables based on which the model makes predictions
- **Target variables** - Variables which the model tries to predict based on available features

Then, we denote the dataset and variables as:
$$
\large 
D = \{(x_1, y_1), \dots, (x_n, y_n)\}
$$
where:
- $\large x_i = (x_{i1}, \dots, x_{id})$ - Features of the $i$-th data sample
- $\large y_i = (y_{i1}, \dots, y_{ik})$ - Target variables of the $i$-th data sample

Or we could write:
$$
\large
x_i = (\underbrace{x_{i1}, \dots, x_{id}}_{\text{Features}}
, \underbrace{y_{i1}, \dots, y_{ik}}_{\text{Target variables}}), \quad
d + k = m
$$
# 

#MachineLearning 