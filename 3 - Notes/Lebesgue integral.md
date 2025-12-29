Tags: [[__Mathematics]], [[_Mathematical_analysis]]
#MathematicalAnalysis #Mathematics 

# Introduction
Lebesgue integral is more general than the Riemann one ([[Riemann integral|link]]). Riemann integral is a special case of the Lebesgue one, and some functions are not Riemann integrable while they are Lebesgue integrable.

Lebesgue integral also calculates the area under the curve of a function.

One of the sections in this document describes the relation between the Lebesgue integral and the Riemann one.
# Notation and shorthands
This document uses notation and shorthands which are described here - [[Mathematical general notations and shorthands|link]].
# Formal definition
Definition consists of 3 parts, where we define Lebesgue measure for:
- Simple function
- Non-negative function
- Any function

***Simple function***
Let $(\Omega, \mathcal{F}, \mu)$ be a measurable space ([[Measure space|link]]) and $s: \Omega \rightarrow [0, \infty)$ be a simple measurable function ([[Measurable function|link]]), that is:
$$
\large
s(\omega) = \sum_{i=1}^n a_i \mathbb{1}_{E_i} (\omega)
$$
where:
- $a_i \ge 0$ 
- $E_i \in \mathcal{F}$ - measurable sets ([[Measurable set|link]])
- $\mathbb{1}_{E_i}(\omega)$ is the indicator function (returns 1 if $\omega \in E_i$)

Lebesgue integral for a simple function is defined as:
$$
\int_\Omega s d\mu = \sum_{i=1}^n a_i \mu(E_i)
$$

***Non-negative function***
Now let $f: \Omega \rightarrow [0, \infty)$ be a measurable function. Lebesgue integral for such a function is defined as:
$$
\int_\Omega f d\mu = \sup\{\int_\Omega s d\mu: 0 \le s \le f, \text{ s - simple function}\}
$$

***Any function***
Now let $f: \Omega \rightarrow \mathbb{R}$ be a measurable function and
$$
f^+ = \max(f, 0) , \quad f^- = \max(-f, 0)
$$
Lebesgue integral for such a function is defined as:
$$
\int_\Omega f d\mu = \int_\Omega f^+ d\mu - \int_\Omega f^- d\mu
$$
# Intuition
If we have a function $f: \mathcal{X} \rightarrow [0, \infty)$, then we can:
- Partition values of $f$ into intervals $[y_{k-1}, y_k)$ 
- Define sets:
$$
E_k = \{x \in X: f(x) \in [y_{k-1}, y_k)\}
$$
- Construct a simple function which approximates $f(x)$ from below:
$$
\large
s(x) = \sum_{k=1}^n y_{k-1} \mathbb{1}_{E_k}(x)
$$
Then Lebesgue integral is:
$$
\int_\Omega s d\mu = \sum_{k=1}^n y_{k-1} \mu(E_k)
$$
So we multiply the height of the height of a strip $y_{k-1}$ by the measure of the region (on the x-axis) $\mu(E_k)$ where the function has that height.
# Multidimensional Lebesgue integral
Let's assume that $(\mathcal{X}_i, \mathcal{F}_i, \mu_i),\ i = 1, \ldots, n$ are measure spaces. The product space is:
$$
(\mathcal{X}_1 \times \ldots \times \mathcal{X}_n, 
\mathcal{F}_1 \otimes \ldots \otimes \mathcal{F}_n, 
\mu_1 \otimes \ldots \otimes \mu_n, )
$$
where:
- $\mathcal{F}_1 \otimes \ldots \otimes \mathcal{F}_n$ is a product $\sigma$-algebra ([[Product sigma algebra|link]])
- $\mu_1 \otimes \ldots \otimes \mu_n$ is a product measure ([[Product measure|link]])

For a function of multiple variables $f: \mathcal{X}_1 \times \ldots \times \mathcal{X}_n \rightarrow \mathbb{R}$, which is measurable with respect to the given product $\sigma$-algebra, multiple Lebesgue integral is defined as:
$$
\Large
\int_{\mathcal{X}_1 \times \ldots \times \mathcal{X}_n} f(x_1, \ldots, x_n) 
d(\mu_1 \otimes \ldots \otimes \mu_n) (x_1, \ldots, x_n)
$$
Or in short:
$$
\Large
\int_{\prod_{i=1}^n \mathcal{X}_i} f(x_{1:n}) d (\mu_{1:n}^{\otimes n}) (x_{1:n})
$$
# Relation to the Riemann integral
If we choose:
- The Lebesgue measure ([[Lebesgue measure|link]]) $\lambda$ as $\mu$ 
- $(\mathbb{R}, \mathcal{B}(\mathbb{R}))$ as measurable space
and function $f$ is Riemann integrable, then its Lebesgue integral gives the same result:
$$
\large
\int_a^b f(x)dx = \int_{[a, b]} f(x) d\lambda(x)
$$
where $\lambda$ is the Lebesgue measure on $\mathbb{R}$.
# Related topics
1. [[Set]]
2. [[Sigma algebra]]
3. [[Product sigma algebra]]
4. [[Measure]]
5. [[Measurable set]]
6. [[Measure space]]
7. [[Measurable function]]
8. [[Product measure]]
9. 
