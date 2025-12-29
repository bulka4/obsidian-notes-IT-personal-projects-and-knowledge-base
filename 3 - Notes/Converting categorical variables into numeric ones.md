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

But data samples from such a dataset can contain categorical variables and, as described here - [[Types of variables used for creating ML models|link]], even if a categorical variable has values written as numbers and they do have an order (ordinal variables), they can't be interpreted as numbers.

Because of that, categorical variables should not be used as an input for a model and, we need to convert them into a numeric variables first.
# Types of numeric inputs for ML models
Numeric variables, used as an input for ML models, can have different number of dimensions, as described here - [[Types of numeric inputs for ML models]].
# Methods
Methods for converting categorical variables into numeric ones include:
- [[Encoding categorical variables]]
- [[Feature embeddings]]

#MachineLearning 