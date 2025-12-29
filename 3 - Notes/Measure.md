Tags: [[__Mathematics]], [[_Mathematical_analysis]]
#MathematicalAnalysis #Mathematics 

# Introduction
A measure is a function that assigns non-negative values to subsets of a given set ([[Set|link]]). Those values might represent size, length, area or probability.
# Formal definition
Let $X$ be a set and $\mathcal{F}$ be a $\sigma$-algebra ([[Sigma algebra|link]]). A measure is a function:
$$
\mu:\mathcal{F} \rightarrow [0, \infty]
$$
such that:
- $\mu(A) \ge 0,\ \forall A \in \mathcal{F}$ 
- $\mu(\emptyset) = 0$ 
- For any countable collection of sets $\{A_i\}_{i=1}^\infty \subseteq \mathcal{F}$ which are pairwise disjoint (i.e. $A_i \cap A_j = \emptyset,\ \forall i,j$):$$
  \mu(\bigcup_{i=1}^\infty) = \sum_{i=1}^\infty \mu(A_i)
  $$
# Examples
Here are a common examples of measure functions:
- Counting measure: $\mu(A) = \text{number of elements in A}$ 
- Lebesgue measure (length): $\mu([a, b]) = b - a$ 
- Probability: $\mathbb{P}(A) = \text{probability that the event A occurs}$ 
# Related topics
1. [[Set]]
2. [[Sets operations and annotations]]
3. [[Sigma algebra]]
 