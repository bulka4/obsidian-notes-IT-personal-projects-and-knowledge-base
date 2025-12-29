Tags: [[__Mathematics]], [[_Probability]]

# Notation and shorthands
This document uses notation and shorthands which are described here - [[Mathematical general notations and shorthands|link]].
# Introduction
Let $(\Omega, \mathcal{F}, P)$ be a probability space ([[Probability space (events, probability measure)|link]]). Events $A, B \in \mathcal{F}$ are said to be independent if:
$$
P(A \cap B) = P(A) \cdot P(B)
$$
# Relation to a conditional probability
If $A$ is independent on $B$, then conditional probability ([[Conditional probability|link]]) of $A$ given $B$ is just a probability of $A$:
$$
P(A \mid B) = \frac{P(A \cap B)} {P(A)} = \frac{P(A) \cdot P(B)} {P(B)} = P(A)
$$
# Joint conditional probability
In case of joint conditional probability ([[Joint conditional probability|link]]), we say that events $A_i$ are independent given $\large B_{1:n}$ and that means:
$$
P(\bigcap_{i=1}^n A_i \mid \bigcap_{i=1}^n B_i) = \prod_{i=1}^n P(A_i \mid \bigcap_{i=1}^n B_i)
$$
Sometimes we additionally add, that $A_i$ depends only on the corresponding $B_i$, and then:
$$
P(A_i \mid \bigcap_{j=1}^n B_j) = P(A_i \mid B_i),\ \forall i
$$
what implies:
$$
P(\bigcap_{i=1}^n A_i \mid \bigcap_{i=1}^n B_i) = \prod_{i=1}^n P(A_i \mid B_i)
$$
When someone says 'events $A_i$ are independent given $B_i$' it might mean that 'events $A_i$ are independent given $\large B_{1:n}$ and additionally $A_i$ depends only on the corresponding $B_i$'.
# Related topics
1. [[Probability space (events, probability measure)]]
2. [[Conditional probability]]
3. [[Joint conditional probability]]

#Mathematics #Probability 