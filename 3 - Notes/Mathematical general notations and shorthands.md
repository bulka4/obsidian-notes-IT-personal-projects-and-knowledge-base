Tags: [[__Mathematics]]

# Introduction
This document explains the most common mathematical annotations which appears in this entire documentation.
# Numbers
## Multiplying numbers (product sign)
The product sign $\prod_{i=1}^n$ is used to indicate a multiplication of multiple numbers, for example:
$$
\prod_{i=1}^n x_i = x_1 \cdot x_2 \cdot \ldots \cdot x_n
$$
And if we have multiple product signs:
$$
\Large
\prod_{x_i \in X_i} \ldots \prod_{x_n \in X_n} \iff \prod_{x_{1:n} \in \prod_{i=1}^n X_i}
$$

It is also used to indicate a cartesian product.
## Adding numbers (sum sign)
The sum sign $\sum_{i=1}^n$ is used to indicate a sum of multiple numbers, for example:
$$
\sum_{i=1}^n x_i = x_1 + x_2 + ... + x_n
$$
And if we have multiple sum signs:
$$
\Large
\begin{align}
\text{1) } & \sum_{x_i \in X_i} \ldots \sum_{x_n \in X_n} \iff \sum_{x_{1:n} \in \prod_{i=1}^n X_i} \\
\text{2) } & \sum_{x_i \in X_i} \ldots \sum_{x_n \in X_n} \iff \sum_{x_{1:n} \in X_{i:n}} \\
\text{2) } & \sum_{x_{i_1} \in X_{i_1}} \ldots \sum_{x_{i_n} \in X_{i_n}} \iff \sum_{x_I \in X_I}, \quad I = \{i_1, \ldots, i_n\} \text{ - set of indexes} \\
\end{align}
$$
# Measures
## Measure product
To write a product of measure we can use this shorthand:
$$
\large
\begin{align}
\text{1) } & \mu^{\otimes n} = \mu \times \ldots \times \mu \\
\text{2) } & \mu^{\otimes n}_{1:n} = \mu_1 \times \ldots \times \mu_n \\
\text{3) } & \bigotimes_{i \in I} \mu_i = \mu_{i_1} \times \ldots \times \mu_{i_n},\quad I = \{i_1, \ldots, i_n\} \text{ - given set of indexes}
\end{align}
$$
## Sigma algebras
To write a product $\sigma$-algebra we can use those shorthands:
$$
\large
\begin{align}
\text{1) } & \bigotimes_{i=1}^n \mathcal{F}_i = \mathcal{F}_1 \otimes \ldots \otimes \mathcal{F}_n \\
\text{2) } & \bigotimes_{i \in I} \mathcal{F}_i = \mathcal{F}_{i_1} \otimes \ldots \otimes \mathcal{F}_{i_n},\quad I = \{i_1, \ldots, i_n\} \text{ - given set of indexes}\\
\end{align}
$$
# Sets
## The 'in' sign
The $\in$ sign tells us that a specific variable belongs to a specific set of numbers, for example:
$$
x \in \{1, 2, 3\}
$$
means that $x$ belongs to the set of numbers $\{1, 2, 3\}$ so it can be equal to any out of those numbers.

And if we have multiple 'in' signs:
$$
\large
x_1 \in X_1 \wedge \ldots \wedge x_n \in X_n \iff x_{1:n} \in \prod_{i=1}^n X_i
$$
or
$$
\large
x_1 \in X_1 \wedge \ldots \wedge x_n \in X_n \iff \bigwedge_{i=1}^n x_i \in X_i
$$
## Set of indexed elements
$$
\large
\{x_1, \dots, x_n\} = \{x_i\}_{i=1}^n
$$
$$
\large
\{x_{i_1}, \dots, x_{i_n}\} = \{x_i\}_{i \in I}, \quad I = \{i_1, \ldots, i_n\}
$$
## Union of sets
Union of sets $A_1 \cup \ldots \cup A_n$ can be shortly written as:
$$
\bigcup_{i=1}^n A_i
$$
## Intersection of sets
Intersection of sets $A_1 \cap \ldots \cap A_n$ can be shortly written as:
$$
\bigcap_{i=1}^n A_i
$$
## Cartesian product (product sign)
To write a cartesian product of sets we can use the product sign like in case of multiplying numbers:
$$
\large
\begin{align}
\text{1) } & \prod_{i=1}^n A_i = A_1 \times \ldots \times A_n \\
\text{2) } & \prod_{i \in I}^n A_i = A_{i_1} \times \ldots \times A_{i_n}, \quad I = \{i_1, \ldots, i_n\} \\
\end{align}
$$
And if we have multiple product signs:
$$
\Large
\prod_{x_i \in X_i} \ldots \prod_{x_n \in X_n} \iff \prod_{x_{1:n} \in \prod_{i=1}^n X_i}
$$
# Logical operators
## The 'exists' sign
The $\exists$ sign means 'exists', for example this notation:
$$
\exists x \in A: x >5
$$
means that there exists such an $x$ in a set $A$ which is bigger than 5.
## The 'For all' sign
The $\forall$ sign means 'for all', for example we can use it to say that the below equation is true for every $x$ which belongs to the set of numbers $\{1, 2, 3\}$:
$$
x < 4,\ \forall x \in \{1, 2, 3\}
$$
## Logical 'or' operator
The "$\vee$" sign means 'or' when specifying logical conditions, for example: $x = 1 \vee x = 5$.

A shorthand for specifying multiple conditions is:
$$
\bigvee_1^n x_i = x'_i
$$
what means:
$$
x_1 = x'_1 \vee \ldots \vee x_n = x'_n
$$
## Logical 'and' operator
The "$\wedge$" sign means 'and' when specifying logical conditions, for example: $x_1 = x'_1 \wedge x_2 = x'_2$.

A shorthand for specifying multiple conditions is:
$$
\bigwedge_1^n x_i = x'_i
$$
what means:
$$
x_1 = x'_1 \wedge \ldots \wedge x_n = x'_n
$$
# Sequence of elements
If we have a long sequence of indexed elements we can use a shorthand like this:
$$
\large
\begin{align}
\text{1) } & x_{1:n} = x_1, \ldots, x_n \\
\text{2) } & x_I = x_{i_1}, \ldots, x_{i_n}, \quad I = \{i_1, \ldots, i_n\} \text{ - chosen set of indexes}
\end{align}
$$
We use it for example when we want to write function arguments:
$$
\large f(x_{1:n}) \iff f(x_1, \ldots, x_n)
$$
or a vector:
$$
\large (x_1, \ldots, x_n) = x_{1:n} \in \prod_{i=1}^n X_i = X_1 \times \ldots \times X_n
$$
# Integrals
## Multiple integrals over sets
If we have a long sequence integrals over sets, we can use a shorthands like this:
$$
\large
\int_{A_1 \times \ldots \times A_n} f(x_1, \ldots, x_n) 
d(\mu_1 \otimes \ldots \otimes \mu_n) (x_1, \ldots, x_n)
\iff
\int_{\prod_{i=1}^n A_i} f(x_{1:n}) d(\mu_{1:n}^{\otimes n}) (x_{1:n})
$$
and
$$
\Large
\int_{A_1} \ldots \int_{A_n} f d\mu_n (x_n) \ldots d\mu_1(x_1) 
\iff 
\int_{A_{1:n}} f d\mu_{n:1}(x_{n:1})
$$
and for given set of indexes:
$$
\Large
\int_{A_{i_1}} \ldots \int_{A_{i_n}} f d\mu_{i_n} (x_{i_n}) \ldots d\mu_{i_1}(x_{i_1}) 
\iff 
\int_{A_I} f d\mu_I(x_I)
,\quad I = \{i_1, \ldots, i_n\}
$$
where:
$$
\Large
\begin{align}
\text{1) } & \prod_{i=1}^n A_i = A_1 \times \ldots \times A_n \\
\text{2) } & \mu_{1:n}^{\otimes n} = \mu_1 \times \ldots \times \mu_n
\end{align}
$$
## Multiple integrals over intervals
If we have a long sequence integrals over intervals with Lebesgue measure, we can use a shorthand like this:
$$
\Large
\int_{a_1}^{b_1} \ldots \int_{a_n}^{b_n} f dx_n \ldots dx_1
\iff \int_{a_{1:n}}^{b_{1:n}} f dx_{n:1}
$$
and for given set of indexes:
$$
\Large
\int_{a_{i_1}}^{b_{i_1}} \ldots \int_{a_{i_n}}^{b_{i_n}} f dx_{i_n} \ldots dx_{i_1}
\iff \int_{a_I}^{b_I} f dx_I
,\quad I = \{i_1, \ldots, i_n\}
$$

#Mathematics 