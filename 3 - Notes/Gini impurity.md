Tags: [[_Information_theory]], [[__Mathematics]]

# Introduction
Gini impurity measures an uncertainty of an outcome of an experiment, how hard it is to predict what will be an outcome of that experiment, as described here - [[Experiment outcome uncertainty and average surprise measures|link]].

Also, we can interpret it, that it measures a probability, that:
- Two experiments will result in different outcomes
- Two elements randomly selected from a dataset will be of a different class

More precisely:
- High Gini impurity -> outcomes are uncertain and hard to predict (many events with a similar, relatively high probabilities)
- Low Gini impurity -> outcomes are predictable, there is a few high-probability events (probability mass is concentrated on a few events)
# Definition
Gini impurity is defined as:
$$
G = \sum_{i \neq j} p_i p_j = \sum_{i=1}^K p_i(1 - p_i) = 1 - \sum_{i=1}^K p_i^2
$$
where:
- $P_X$ is a probability distribution of a discrete random variable $X$ 
- $p_i = P_X(x_i) = P(X = x_i),\ \forall i = 1, \ldots, K$ 
- $\{x_i\}_{i=1}^K$ - Set of all possible values of $X$ 
# Interpretation
More about interpretation of Gini impurity as a measure of uncertainty can be found here - [[Experiment outcome uncertainty and average surprise measures|link]].

#InformationTheory #Mathematics 