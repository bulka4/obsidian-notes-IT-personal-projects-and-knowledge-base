Tags: [[__Machine_Learning]]

# Introduction
Models for a binary classification, where there are only two possible classes $y \in \{0, 1\}$, for a given data point (input), assigns probability to both categories that this is the right category for the given data point.

The decision / classification threshold indicates, how high this probability needs to be in order to classify given data point to one of those classes.

If we mark:$$
\begin{gathered}
p(x) = P(y = 1 | x) \\
1 - p(x) = P(y = 0 | x)
\end{gathered}
$$ then prediction $\hat{y}$ is designated in the following way:
$$
\hat{y} = 
\begin{cases}
1,\ \text{if} \ p(x) > \text{classification theshold} \\
0,\ \text{if} \ p(x) <= \text{classification theshold}
\end{cases}
$$
# Related topics
- Classification - [[Classification models|link]]

#MachineLearning 