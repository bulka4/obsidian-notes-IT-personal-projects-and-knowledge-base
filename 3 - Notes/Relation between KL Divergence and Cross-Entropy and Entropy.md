Tags: [[__Machine_Learning]]

# Introduction
KL Divergence ([[KL Divergence|link]]) formula consists of formulas for the Cross-Entropy ([[Cross-Entropy|link]]) and Entropy ([[Entropy|link]]).

Minimizing Cross-Entropy is equivalent to minimizing KL Divergence.
# Relation to Cross-Entropy and Entropy
KL Divergence formula consist of formulas for the Cross-Entropy and Entropy.

We can write the KL Divergence as:
$$
\large
D_{KL}(p \lVert q) = 
-\mathbb{E}_{P(Y \mid X = x)} (\log(q(Y \mid x))) - 
(-\mathbb{E}_{P(Y \mid X = x)} (\log( p(Y \mid x))))
= H(P, Q) - H(P)
$$
where we use the notation:
$$
\large
\begin{align}
 & H(P, Q) = -\mathbb{E}_{P(Y \mid X = x)} (\log(q(Y \mid x))) \\
 & H(P) = -\mathbb{E}_{P(Y \mid X = x)} (\log( p(Y \mid x)))
\end{align}
$$
where:
- $H(P, Q)$ is the Cross-Entropy ([[Cross-Entropy|link]])
- $H(P)$ is the Entropy ([[Entropy|link]])

So minimizing Cross-Entropy ($H(P, Q)$) is equivalent to minimizing KL Divergence $D_{KL}(p \mid\mid q)$, that is minimizing the difference between the true probability distribution function $p$ and the one defined by the statistical model $q$.
# Interpretation


#MachineLearning 