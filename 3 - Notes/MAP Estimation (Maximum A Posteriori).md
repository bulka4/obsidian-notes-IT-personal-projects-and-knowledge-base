Tags: [[__Machine_Learning]]

# Introduction
MAP estimation is a way of estimating model parameters using **Bayes’ rule**.  
It combines:
- **What the data suggests** (likelihood)
- **What we believed before seeing the data** (prior)

and picks the parameter value that is **most probable after seeing the data**.
# Bayes' Rule for parameters
Posterior distribution over parameters $\theta$ is:
$$
p(\theta \mid D) = \frac{p(D \mid \theta) p(\theta)}{p(D)}
$$
where:
- $p(\theta)$ - Prior - What we believe about parameters (their probability distribution ([[Probability distribution|link]])) before seeing data
- $p(\theta \mid D)$ - Posterior - Our updated belief about parameters after seeing data
- $p(D \mid \theta)$ - Likelihood ([[Likelihood function|link]]) - How well parameters explain the observed data
- $p(D)$ - Constant

MAP chooses parameter values that maximized the posterior:
$$
\theta_{MAP} = \text{arg} \max_\theta p(\theta \mid D)
$$
Using the Bayes' Rule that becomes:
$$
\theta_{MAP} = \text{arg} \max_\theta p(D \mid \theta) p(\theta)
$$
We don't include here $p(D)$ becomes it does not depend on $\theta$.
# Log posterior
We usually maximize the **log posterior** as it is equivalent and simpler to do:
$$
\theta_{MAP} = \text{arg} \max_\theta [\log(p(D \mid \theta) + \log(p(\theta))]
$$
# Relation to minimizing loss with regularization
How MAP is related to minimizing a loss function with regularization is described here - [[Relation between MAP and minimizing loss with regularization]].
# Relation to L1 and L2 regularizations
How MAP is related to to L1 and L2 regularizations is described here - [[Relation of L1 and L2 regularizations to MAP]]

#MachineLearning 