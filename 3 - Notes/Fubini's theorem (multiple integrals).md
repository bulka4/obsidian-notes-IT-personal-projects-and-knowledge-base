Tags: [[__Mathematics]], [[_Mathematical_analysis]]
#MathematicalAnalysis #Mathematics 

# Introduction

# Notation and shorthands
This document uses notation and shorthands which are described here - [[Mathematical general notations and shorthands|link]].
# Fubini's theorem
Let $(\mathcal{X}_i,\ \mathcal{F}_i,\ \mu_i),\ i = 1, \ldots, n$ be $\sigma$-finite measure spaces ([[Sigma finite measure space|link]]) and $f: \prod_{i=1}^n \mathcal{X}_i \rightarrow \mathbb{R}$ be integrable function, i.e. 
$$
\large
\int_{\prod_{i=1}^n \mathcal{X}_i} |f| d(\mu_1 \otimes \ldots \otimes \mu_n) < \infty
$$
then for any measurable sets ([[Measurable set|link]]) $A_i \in \mathcal{F}$:
$$
\Large
\int_{A_1 \times \ldots \times A_n} f(x_1, \ldots, x_n) 
d(\mu_1 \otimes \ldots \otimes \mu_n) (x_1, \ldots, x_n) = 
\int_{A_1} \ldots \int_{A_n} f d\mu_n(x_n) \ldots d\mu_1(x_1)
$$
Or in short:
$$
\Large
\int_{\prod_{i=1}^n A_i} f(x_{1:n}) d(\mu_{1:n}^{\otimes n}) (x_{1:n}) = \int_{A_{1:n}} f(x_{1:n}) d\mu_{n:1}(x_{n:1})
$$ 
# Related topics
1. [[Mathematical general notations and shorthands]]
2. [[Measure space]]
3. [[Measurable set]]
