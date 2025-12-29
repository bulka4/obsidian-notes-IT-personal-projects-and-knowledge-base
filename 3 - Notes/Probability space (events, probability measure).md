Tags: [[_Probability]], [[__Mathematics]]

# Introduction
Probability space is a triple $(\Omega, \mathcal{F}, P)$ which defines what are all the possible events and what probabilities are being assigned to them.

It is the backbone of the entire probability theory. It is used in all the other definitions.
# Formal definition
Probability space is a triple $(\Omega, \mathcal{F}, P)$ where:
- $\Omega$ - A sample space
- $\mathcal{F}$ - A collection of events
- $P$ - A probability measure

Each of the elements of the probability space is explained in sections below.
# Sample space $\Omega$
The sample space $\Omega$ is a set ([[Set|link]]) which represents a sample space, that is a set of all possible outcomes of a random experiment.
# Collection of events $\mathcal{F}$
The $\sigma$-algebra ([[Sigma algebra|link]]) $\mathcal{F}$ represents events. That is a collection of all subsets of the sample space $\Omega$.
# Probability measure P
The probability measure $P$ is a measure ([[Measure|link]]) used for calculating probabilities. It is a function:
$$
P: \mathcal{F} \rightarrow [0, 1]
$$
which assigns values from $[0, 1]$ to each event (a set from the $\sigma$-algebra $\mathcal{F}$).

By definition, it has the following properties:
- $\mathbb{P} (\Omega) = 1$ 
- For any countable sequence of events $A_1, A_2, ... \in \mathcal{F}$ that are disjoint (i.e. $A_i \cap A_j = \emptyset,\ \forall i, j)$:
$$
\mathbb{P}(\bigcup_{i=1}^\infty A_i) = \sum_{i=1}^\infty \mathbb{P}(A_i)
$$
# Probability of an event
Probability of an event is denoted as $P(A)$, so that is a value of the probability measure $P$ for a set (event) from the $\sigma$-algebra $\mathcal{F}$.
# Related topics
1. [[Set]]
2. [[Sigma algebra]]
3. [[Measure]]

 #Probability #Mathematics