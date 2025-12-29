Tags: [[__Machine_Learning]]

# Introduction
In machine learning, we usually minimize a loss instead of maximizing probability in order to train a model as described here - [[Loss functions]].

Maximizing log posterior ([[MAP Estimation (Maximum A Posteriori)|link]]) is equivalent to minimizing **negative log posterior**:
$$
\theta_{MAP} = \text{arg} \min_\theta [-\log(p(D \mid \theta) - \log(p(\theta))]
$$
So MAP is equivalent to minimizing a loss function with regularization ([[Regularization|link]]):
$$
\text{arg} \min_\theta(Loss(\theta) + \text{Regularization penalty})
$$
Additionally, regularization penalty can be interpreted as a measure of how 'surprised' we are by observing model parameters $\theta$ obtained from training the model, according to our belief about parameters $\theta$ described by the prior $p$.
# Interpretation
## Loss function (negative log-likelihood)
This component from the negative log posterior formula:
$$
-\log(p(D \mid \theta)
$$
can be interpreted as a loss function.

It is the negative log-likelihood ([[Likelihood function|link]]) formula, from which we can derive a loss function, e.g. MSE or Cross-Entropy, as described in documents below:
- MSE - [[MSE relation to MLE (Maximum Likelihood Estimation)|link]]
- Cross-Entropy - [[Relation of Cross-Entropy to the Maximum Likelihood Estimation|link]] 
## Regularization penalty
This component from the negative log posterior formula:
$$
- \log(p(\theta))
$$
can be interpreted as a regularization penalty ([[Regularization|link]]).

From that formula we can derive L1 and L2 regularizations as described here - [[Relation of L1 and L2 regularizations to MAP|link]] 
### Relation to the surprise measure
Let's remind that:
- Prior $p(\theta)$ is what we believe about parameters before seeing data as described here - [[MAP Estimation (Maximum A Posteriori)|link]]
- $-\log(p_X(x))$ can be interpreted as a measure of 'surprise' of observing the event $X = x$ according to the probability distribution function $p_X$ as described here - [[Surprise measure|link]]

In that case, regularization penalty can be interpreted as a measure of how 'surprised' we are by observing model parameters $\theta$ obtained from training the model, according to our belief about parameters $\theta$ described by the prior $p$.

If we see parameters $\theta$ which has low probability according to the prior $p$, that is $p(\theta)$ is low, that means that we are surprised and surprise measure $- \log(p(\theta))$ (which is a regularization penalty) is big.

So regularization penalty, forces parameters $\theta$ to be more likely according to the prior $p$, so we are less surprised when we see parameters after training a model.

#MachineLearning 