Tags: [[__Mathematics]], [[_Probability]]

# Notation and shorthands
This document uses notation and shorthands which are described here - [[Mathematical general notations and shorthands|link]].
# Introduction
When we have a set of random variables ([[Random variable|link]]) $Y_1, \ldots, Y_n$, and we know their joint conditional probability distribution function ([[Marginal probability distribution function|link]]) then we can use **marginalization** in order to obtain marginal conditional probability distribution function for a subset of those variables, $\large Y_I = (Y_i)_{i \in I}$ where $I$ is a set of our chosen indexes.
# Formal definition
Let's assume, that:
- We have multivariate random variables ([[Multivariate random variable|link]]):
	- $Y = (Y_1, \ldots, Y_n): (\Omega, \mathcal{F}) \rightarrow (\mathcal{Y}_1 \times \ldots \times \mathcal{Y}_n,\ \mathcal{B}_{\mathcal{Y}_1} \otimes \ldots \otimes \mathcal{B}_{\mathcal{Y}_n})$ 
	- $X = (X_1, \ldots, X_m): (\Omega, \mathcal{F}) \rightarrow (\mathcal{X}_1 \times \ldots \times \mathcal{X}_m,\ \mathcal{B}_{\mathcal{X}_1} \otimes \ldots \otimes \mathcal{B}_{\mathcal{X}_m})$
- $\Large P_{Y_{1:n} \mid X_{1:m}}$ - Conditional probability distribution of $\large Y_{1:n}$ given $\large X_{1:m}$ ([[Probability distribution|link]]) with respect to a product measure   
$$
\large
\mu = \mu_1 \otimes \ldots \otimes \mu_n = \mu_{1:n}^{\otimes n}
$$
on the product space  
$$
(\mathcal{Y}_1 \times \ldots \times \mathcal{Y}_n,\ \mathcal{B}_{\mathcal{Y}_1} \otimes \ldots \otimes \mathcal{B}_{\mathcal{Y}_n})
$$
- $I \subseteq \{1, \ldots, n\}$ - Chosen subset of indexes with $I^c = \{1, \ldots, n\} \setminus I$ as its complement (remaining indexes)

If $\Large P_{Y_{1:n} \mid X_{1:m}}$ is absolutely continuous with respect to the measure $\mu$, then marginal probability distribution ([[Marginal probability distribution|link]]) $\Large P_{Y_I \mid X_{1:m}}$ is also absolutely continuous with respect to the corresponding marginal product measure:
$$
\large
\mu_I = \bigotimes_{i \in I} \mu_i
$$
and its probability distribution function is:
$$
\Large
p_{Y_I \mid X_{1:m}}(y_I \mid x_{1:m}) = \int_{\mathcal{Y}_{I^c}} p_{Y_{1:n} \mid X_{1:m}}(y_I, y_{I^c} \mid x_{1:m}) d\mu_{I^c}(y_{I^c})
$$

This operation of creating $\Large p_{Y_I \mid X_{1:m}}(y_I \mid x_{1:m})$ is called **marginalization**.
# Continuous random variables
If $Y = (Y_1, \ldots, Y_n)$ are continuous random variables, we usually use the Lebesgue measure as $\mu$ and $\mathcal{Y} = \mathcal{Y}_1 \times \ldots \times \mathcal{Y}_n = \mathbb{R}^n$. 

Then marginalization formula looks like that:
$$
\Large
p_{Y_I \mid X_{1:m}}(y_I \mid x_{1:m}) = \int_{\mathbb{R}^{|I^c|}} p_{Y_{1:n} \mid X_{1:m}}(y_I, y_{I^c} \mid x_{1:m}) dy_{I^c}
$$
where $|I^c|$ is a number of elements in the set $I^c$.
## Example
When we have two continuous random variables defined on $\mathbb{R}$ and we use the Lebesgue measure, then marginalization equation looks like that:
$$
\large
p_{Y \mid X}(y_1 \mid x) = \int_{\mathbb{R}} p_{Y_1, Y_2 \mid X}(y_1, y_2 \mid x)dy_2
$$
# Discrete random variables
If $Y = (Y_1, \ldots, Y_n)$ are discrete random variables, we usually use the Counting measure as $\mu$ and $\mathcal{Y} = \mathcal{Y}_1 \times \ldots \times \mathcal{Y}_n = \mathbb{R}^n$.

Then marginalization formula looks like that:
$$
\Large
p_{Y_I \mid X_{1:m}}(y_I \mid x_{1:m}) = \sum_{y_{I^c} \in \mathcal{Y}_{I^c}} p_{Y_{1:n} \mid X_{1:m}}(y_I, y_{I^c} \mid x_{1:m})
$$
## Example
When we have two discrete random variables defined on $\mathbb{R}$
$$
(Y_1, Y_2): \Omega \rightarrow \mathcal{Y}_1 \times \mathcal{Y}_2
$$
and we use the counting measure, then marginalization equation looks like that:
$$
\Large
p_{Y \mid X}(y_1 \mid x) = \sum_{{y_2} \in \mathcal{Y}} p_{Y_1, Y_2 \mid X}(y_1, y_2 \mid x)
$$
# Mix of continuous and discrete random variables
If $Y = (Y_D, Y_C)$ is a mix of continuous and discrete random variables, where:
- $Y_D = (Y_d)_{d \in D}$ - Discrete random variable (can be a multivariate)
- $Y_C = (Y_c)_{c \in C}$ - Continuous random variable (can be a multivariate)
- $D, C$ - Disjoint sets of indexes of discrete (D) and continuous (C) random variables ($D \cup C = \{1, \ldots, n\}$)

Joint probability distribution $\Large P_{Y_{1:n} \mid X_{1:m}}$ is defined on the product measurable space $(\mathcal{X}_D \times \mathcal{X}_C, \mathcal{B}_{\mathcal{X}_D} \otimes \mathcal{B}_{\mathcal{X}_C})$

We will use a product measure which is a mix of the Counting $\upsilon_d$ and Lebesgue measures $\lambda_c$:
$$
\mu = \bigotimes_{d \in D} \upsilon_d \otimes \bigotimes_{c \in C} \lambda_c
$$
Let's assume, that:
- $I \subseteq D \cup C$ - Subset of variable indexes with $I^c$ as its complement
- $I_d = I \cap D$ - Subset of indexes for discrete variables
- $I_c = I \cap C$ - Subset of indexes for continuous variables
- $I^c_c, I^c_d$ - Complements of $I_c, I_d$ 

Then formula for marginalization becomes:
$$
\Large
p_{Y_I \mid X_{1:m}}(y_I \mid x_{1:m}) = \sum_{y_{I^c_d} \in \mathcal{Y}_{I^c_d}} \int_{\mathcal{Y}_{I^c_c}}
p_{Y_{1:n} \mid X_{1:m}}(y_I, y_{I^c} \mid x_{1:m}) d\lambda_{I^c_c}(y_{I^c_c})
$$
# Related topics
1. 

#Mathematics #Probability 