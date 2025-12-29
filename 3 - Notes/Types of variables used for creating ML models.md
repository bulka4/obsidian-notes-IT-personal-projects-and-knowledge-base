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

Below are described different types of variables which we can have in such a dataset.
# Categorical variables
Categorical variables are the ones with a countable set ([[Countable and uncountable set|link]]) of possible values. 

Their values can be anything - numbers, text or yet something else. But even if those are numbers, we can't treat them like numbers, performing calculations on them doesn't make sense.

For example, a categorical variable can have numeric values which represent different categories, such as:
- 1 = 'mouse'
- 2 = 'dog'
- 3 = 'cat'
Here it doesn't make sense to say that 'mouse' + 'dog' = 'cat' or that 'dog' is twice 'mouse'. So even though those are numbers, they can't be treated like numbers.

Categorical variables are further split into two sub-categories:
- Nominal - Without order / hierarchy
- Ordinal - With order / hierarchy
## Nominal variables
Nominal variables are a type of categorical variables which don't have any order or hierarchy.

Like in our previous example, with numeric values representing different categories:
- 1 = 'mouse'
- 2 = 'dog'
- 3 = 'cat'
we don't have any hierarchy or order, we can't say for example that 'dog' > 'cat' (those values are not about the size).
## Ordinal variables
Ordinal variables are a type of categorical variables which do have an order or hierarchy. We can compare those values, which are bigger.

For example, we might have an ordinal variable indicating education level:
- 1 = 'high school'
- 2 = 'university'

Here we have an order, we can say that 'high school' = 1 < 2 = 'university'. 

But they still can't be interpreted exactly like numbers, because they indicate only an order, not a magnitude.

For example, a difference between those values:
$$
2 - 1 = 1
$$
doesn't mean that the difference between 'university' and 'high school' equals 'high school'.
# Numeric variables
Variables that describe a measurable quantity as a number, like 'how many', 'how much'. 

They split further into continuous and discrete variables.
## Continuous variables
Continuous variables have an uncountable ([[Countable and uncountable set|link]]) set of all the possible values.
## Discrete variables
Discrete variables have a countable ([[Countable and uncountable set|link]])  set of all the possible values.
### Binary variables
Binary variables are a special case of a discrete variables, those are ones which have only two possible values: zero and one.

#MachineLearning 