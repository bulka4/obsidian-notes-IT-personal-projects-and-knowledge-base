Tags: [[__Mathematics]], [[_Mathematical_analysis]]
#MathematicalAnalysis #Mathematics 

# Introduction
A discrete measure ([[Measure|link]]) represents a mass concentrated at specific points. Each element of a set ([[Set|link]]) has assigned some non-zero mass by that measure.

So any set can be represented as a sum of masses of elements it contain, i.e. a measure of a set is a sum of measures of its elements.

An example of a discrete measure is the counting measure, which assigns to a set a number of its elements:
$$
\mu(A) = \#A \text{ (number of elements in A)}
$$
# Formal definition
A measure $\mu$ on $(\mathcal{X}, \mathcal{B}_{\mathcal{X}})$ is called discrete if there exists a countable set ([[Set|link]]) $\large \{x_i\}_{i \in I} \subseteq \mathcal{X}$ and non-negative weights $a_i > 0$ such that for every measurable set $A$:
$$
\large
\mu(A) = \sum_{i \in I} a_i \mathbb{1}\{x_i \in A\}
$$
where $\mathbb{1}\{x_i \in A\}$ is the indicator function which equals to 1 when $x_i \in A$ and 0 otherwise.
# Related topics
1. [[Measure]]
2. [[Set]]
