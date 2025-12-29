Tags: [[__Mathematics]], [[_Mathematical_analysis]]
#MathematicalAnalysis #Mathematics 

# Introduction
Lebesgue measure generalizes the notion of length, area and volume for sets in $\mathbb{R}^n$.
# Formal definition
Let's assume, that $(\mathbb{R}^n, \mathcal{B}({\mathbb{R}^n}))$ is a measurable space ([[Measurable space|link]]), where $\mathcal{B}({\mathbb{R}^n})$ is the Borel $\sigma$-algebra ([[Borel sigma algebra|link]]).

***Outer measure $\lambda^*$***
For any $A \subseteq \mathbb{R}^n$ we define outer measure $\lambda ^*$ as:
$$
\large
\lambda^*(A) = \inf\{\sum_{i=1}^\infty vol(R_i): A \subseteq \bigcup_{i=1}^\infty R_i,\ R_i = \prod_{j=1}^n(a_{ij}, b_{ij})\}
$$
where 
- $\prod_{j=1}^n(a_{ij}, b_{ij}) = (a_{i1}, b_{i1}) \times \ldots \times (a_{in}, b_{in})$ - A rectangle (cartesian product ([[Cartesian product|link]]))
- $vol(R_i) = \prod_{i=1}^n (a_{ij}, b_{ij})$ - Volume (area) of a rectangle

So measure of the set $A$ is the smallest possible volume (area) of a rectangle which covers that set.


***Measurable sets***
Set $E \subseteq \mathbb{R}^n$ is Lebesgue measurable if for all $A \subseteq \mathbb{R}^n$:
$$
\lambda^*(A) = \lambda^*(A \cap E) + \lambda^*(A \setminus E)
$$
Then we define the Lebesgue measure as:
$$
\lambda(E) = \lambda^*(E)
$$
for any measurable set $E$.
# Properties
- For $\mathbb{R}$, we have $\lambda([a, b]) = b - a$ 
- For $\mathbb{R}^n$, we have $\large \lambda(\prod_{i=1}^n [a_i, b_i]) = \prod_{i=1}^n (b_i - a_i)$ 
- if $A_i$ are disjoint, then $\large \lambda(\bigcup_i A_i) = \sum_i \lambda(A_i)$ 
# Related topics
1. [[Measurable space]]
2. [[Borel sigma algebra]]
