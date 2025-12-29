Tags: [[__Mathematics]], [[_Probability]]

# Notation and shorthands
This document uses notation and shorthands which are described here - [[Mathematical general notations and shorthands|link]].
# Introduction
When we have a set of random variables ([[Random variable|link]]) $X_1, \ldots, X_n$, and we know their joint probability distribution function ([[Marginal probability distribution function|link]]) then we can use **marginalization** in order to obtain marginal probability distribution function for a subset of those variables, $\large X_I = (X_i)_{i \in I}$ where $I$ is a set of our chosen indexes.
# Formal definition
Let's assume, that:
- $X = (X_1, \ldots, X_n): (\Omega, \mathcal{F}) \rightarrow (\mathcal{X}_1 \times \ldots \times \mathcal{X}_n,\ \mathcal{B}_{\mathcal{X}_1} \otimes \ldots \otimes \mathcal{B}_{\mathcal{X}_n})$ - Multivariate random variable ([[Multivariate random variable|link]])
- $\Large P_{X_{1:n}}$ - Probability distribution ([[Probability distribution|link]]) for $X_1, \ldots, X_n$ with respect to a product measure   
$$
\large
\mu = \mu_1 \otimes \ldots \otimes \mu_n = \mu_{1:n}^{\otimes n}
$$
on the product space  
$$
(\mathcal{X}_1 \times \ldots \times \mathcal{X}_n,\ \mathcal{B}_{\mathcal{X}_1} \otimes \ldots \otimes \mathcal{B}_{\mathcal{X}_n})
$$
- $I \subseteq \{1, \ldots, n\}$ - Chosen subset of indexes with $I^c = \{1, \ldots, n\} \setminus I$ as its complement (remaining indexes)

If $\Large P_{X_{1:n}}$ is absolutely continuous with respect to the measure $\mu$, then marginal probability distribution ([[Marginal probability distribution|link]]) $\Large P_{X_I}$ is also absolutely continuous with respect to the corresponding marginal product measure:
$$
\large
\mu_I = \bigotimes_{i \in I} \mu_i
$$
and its probability distribution function is:
$$
\Large
p_{X_I}(x_I) = \int_{\mathcal{X}_{I^c}} p_{X_{1:n}}(x_I, x_{I^c}) d\mu_{I^c}(x_{I^c})
$$

This operation of creating $p_{X_I}(x_I)$ is called **marginalization**.
# Continuous random variables
If $X = (X_1, \ldots, X_n)$ are continuous random variables, we usually use the Lebesgue measure as $\mu$ and $\mathcal{X} = \mathcal{X}_1 \times \ldots \times \mathcal{X}_n = \mathbb{R}^n$. 

Then marginalization formula looks like that:
$$
\Large
p_{X_I}(x_I) = \int_{\mathbb{R}^{|I^c|}} p_{X_{1:n}}(x_I, x_{I^c}) dx_{I^c}
$$
where $|I^c|$ is a number of elements in the set $I^c$.
## Example
When we have two continuous random variables defined on $\mathbb{R}$ and we use the Lebesgue measure, then marginalization equation looks like that:
$$
p_X(x) = \int_{\mathbb{R}} p_{X, Y}(x, y)dy
$$
# Discrete random variables
If $X = (X_1, \ldots, X_n)$ are discrete random variables, we usually use the Counting measure as $\mu$ and $\mathcal{X} = \mathcal{X}_1 \times \ldots \times \mathcal{X}_n = \mathbb{R}^n$.

Then marginalization formula looks like that:
$$
\Large
p_{X_I}(x_I) = \sum_{x_{I^c} \in \mathcal{X}_{I^c}} p_{X_{1:n}}(x_I, x_{I^c})
$$
## Example
When we have two discrete random variables defined on $\mathbb{R}$
$$
(X, Y): \Omega \rightarrow \mathcal{X} \times \mathcal{Y}
$$
and we use the counting measure, then marginalization equation looks like that:
$$
\Large
p_{X}(x) = \sum_{{y} \in \mathcal{Y}} p_{X, Y}(x, y)
$$
# Mix of continuous and discrete random variables
If $X = (X_D, X_C)$ is a mix of continuous and discrete random variables, where:
- $X_D = (X_d)_{d \in D}$ - Discrete random variable (can be a multivariate)
- $X_C = (X_c)_{c \in C}$ - Continuous random variable (can be a multivariate)
- $D, C$ - Disjoint sets of indexes of discrete (D) and continuous (C) random variables ($D \cup C = \{1, \ldots, n\}$)

Joint probability distribution $\Large P_{X_{1:n}}$ is defined on the product measurable space $(\mathcal{X}_D \times \mathcal{X}_C, \mathcal{B}_{\mathcal{X}_D} \otimes \mathcal{B}_{\mathcal{X}_C})$.

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
p_{X_I}(x_I) = \sum_{x_{I^c_d} \in \mathcal{X}_{I^c_d}} \int_{\mathcal{X}_{I^c_c}}
p_{X_{1:n}}(x_I, x_{I^c}) d\lambda_{I^c_c}(x_{I^c_c})
$$
# Related topics
1. 

#Mathematics #Probability 