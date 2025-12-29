Tags: [[_Information_theory]], [[__Mathematics]]
# Notation and shorthands
This document uses notation and shorthands which are described here - [[Mathematical general notations and shorthands|link]].
# Introduction
Cross-Entropy is related to uncertainty of an experiment outcome and surprise measure. We can learn more about them here - [[Experiment outcome uncertainty and average surprise measures]].

Cross-Entropy measures what is a difference between two probability distributions ([[Probability distribution|link]]).

It measures how surprised, on average, we are by experiment outcomes when using probability distribution $Q$, weighted by how likely are those outcomes according to the probability distribution $P$.

Low Cross-Entropy indicates that both distributions assign high probabilities to the same events, but it doesn't tell us too much about situations, when distribution $Q$ assigns high probabilities to events which are unlikely according to $P$.

We usually assume, that distribution $P$ is the true one, and $Q$ is defined by a model which we want to train.

Cross-Entropy is related to Maximum Likelihood Estimation (MLE) and KL Divergence like described in those documents:
- [[Relation of Cross-Entropy to the Maximum Likelihood Estimation]]
- [[Relation between KL Divergence and Cross-Entropy and Entropy]]

Also Cross-Entropy can be used to train classification machine learning models as described here - [[Cross-Entropy for classification]].
# Cross-Entropy general formula
Let's assume, that:
- $P, Q$ - Probability distributions ([[Probability distribution|link]]) for a random variable $X: \Omega \rightarrow (\mathcal{X}, \mathcal{B}_{\mathcal{X}})$ ([[Random variable|link]])
- $P$ is absolutely continuous w.r.t $Q$ 
- Both measure $P$ and $Q$ are absolutely continuous w.r.t the measure $\mu$ 

The Cross-Entropy is defined using an expected value ([[Expected value|link]]):
$$
H(P, Q) = \mathbb{E}_{P(X)}(-\log(\frac{dQ}{d\mu}(X)))
$$
or in the integral form:
$$
H(P, Q) = -\int_\mathcal{X} \frac{dP}{d\mu}(x) (-\log(\frac{dQ}{d\mu}(x))) d\mu(x)
$$
where $\large \frac{dP}{d\mu}, \frac{dQ}{d\mu}$ are Radon-Nikodym derivatives (probability distribution functions ([[Probability distribution (density, mass) function|link]]). Their existence is guaranteed by the Radon-Nikodym theorem because of the absolute continuity condition.

We usually assume, that $P$ is the true probability distribution and $Q$ is defined by a statistical model.

Value $(-\log(\frac{dQ}{d\mu}(x)))$ is called a 'surprise measure' as explained here - [[Surprise measure]].
# Relation to Entropy
Note, that if we use the distribution $P$ as the distribution $Q$ (i.e. we set $P = Q$), then Cross-Entropy becomes Entropy ([[Entropy|link]]):
$$
H(P, P) = \mathbb{E}_{P(X)}(-\log(\frac{dP}{d\mu}(X))) = H(P) = \text{Entropy}
$$
# Conditional probability
We can also consider Cross-Entropy in case of conditional probability for two random variables $Y \mid X$.

Here we have two options - to consider the condition $X$ as fixed or non fixed.
## Non-fixed condition
In case when the condition $X$ is not fixed, both variables $X, Y$ are random. In that case, we use probability distributions:
- $P_{X, Y}$ - Joint probability distribution of $(X, Y)$, where:
	- $P_{X, Y}(\cdot, \cdot)$ - function of 2 arguments
	- $P_{X, Y}(A, B) = P(X \in A \wedge Y \in B)$ - joint probability using probability measure $P$ 
- $Q_{Y \mid X}$ - Conditional probability distribution ([[Conditional probability distribution|link]]) of $Y \mid X$, where:
	- $Q_{Y \mid X}(\cdot, \cdot)$ - function of two arguments ($X$ is not fixed)
	- $Q_{Y \mid X}(A, x) = Q(Y \in A \mid X = x)$ - conditional probability using probability measure $Q$ 

We usually assume, that $P$ is the true probability distribution and $Q$ is defined by a statistical model.

We can write Cross-Entropy formula as:
$$
H(P, Q) = \mathbb{E}_{P(X, Y)}(-\log(\frac{dQ}{d\mu}(Y \mid X)))
$$
where $\large \frac{dQ}{d\mu}(y, x)$ is a conditional probability distribution function, where both $x, y$ are arguments.
## Fixed condition
In case when the condition $X = x$ is fixed, we use conditional probability distributions ([[Conditional probability distribution|link]]) $\large P_{Y \mid X = x}$ and $\large Q_{Y \mid X = x}$, where:
- $\large P_{Y \mid X = x}(\cdot)$ is a function of a single argument
- $\large P_{Y \mid X = x}(A) = P(Y \in A \mid X = x)$ for probability measure $P$ 
- The same for $Q$ 

We usually assume, that $P$ is the true probability distribution and $Q$ is defined by a statistical model.

we can write Cross-Entropy formula as:
$$
\large
H(P, Q) = \mathbb{E}_{P(Y \mid X = x)}(-\log(\frac{dQ}{d\mu}(Y \mid x)))
$$
where:
$$
\large \frac{dQ}{d\mu}(y \mid x) = \frac{dQ(\cdot \mid x)}{d\mu}(y)
$$
is a conditional probability distribution function with fixed $x$, only $y$ is an argument.
# Cross-Entropy for different types of random variables
Below sections describe how Cross-Entropy formula looks like in case of different types of random variables ([[Types of random variables|link]]):
- Discrete
- Continuous
## Discrete random variables
In case when $X$ is a discrete random variable, probability distributions are always absolutely continuous w.r.t the Counting measure $\mu$ ([[Counting measure|link]]).

Let's denote:
$$
\large \frac{dP}{d\mu}(x) = P(x), \quad \frac{dQ}{d\mu}(x) = Q(x)
$$
Then:
$$
H(P, Q) = -\int_\mathcal{X} P(x) \log Q(x) d\mu(x)
$$
and for the Counting measure $\mu$, integral becomes a sum:
$$
H(P, Q) = -\sum_{x \in \mathcal{X}} P(x) \log Q(x)
$$
## Continuous random variables
In case when $X$ is a continuous random variable, if both measure $P$ and $Q$ are absolutely continuous w.r.t the Lebesgue measure $\mu$ ([[Lebesgue measure|link]]), then integral becomes a Riemann integral:
$$
\large
H(P, Q) = -\int_{\mathbb{R}^n} p(x) \log q(x) dx
$$
where:
$$
\large \frac{dP}{d\mu}(x) = p(x), \quad \frac{dQ}{d\mu}(x) = p(x)
$$
# Interpretation
***Recollection***
At first let's remind, that Cross-Entropy is defined as an negative expected value of log-probabilities of observing different realizations of $X$ according to $Q$:
$$
\text{Cross-Entropy} = \mathbb{E}_{P(X)}(-\log(q(X))) = \int_\mathcal{X} p(x) (-\log(q(x))) d\mu(x)
$$
## Uncertainty and average surprise
Interpretation of Cross-Entropy is related to uncertainty of an experiment outcome and its average surprise. We can learn more about those concepts from here - [[Experiment outcome uncertainty and average surprise measures]].
## Weighting a surprise
Cross-Entropy formula contains a surprise measure:
$$
-\log(q(x))
$$
which is is weighted by $p(x)$.

That means that values $-\log(q(x))$ for those $x$ for which $p(x)$ is high, contribute more to the total value of Cross-Entropy.

So Cross-Entropy is low, if $-\log(q(x))$ are low for those $x$, for which $p(x)$ is high.

In other words, Cross-Entropy is low, if outcomes (realizations of $X$) which are likely according to the distribution $P$, are also likely according to the distribution $Q$.
## What Cross-Entropy measures
We usually use as $Q$ probability distribution defined by a statistical model and $P$ indicates the true probability distribution.

Cross-Entropy measures how 'surprised', on average, we are by experiment outcomes (observations of $X$) according to the modeled probability distribution $Q$, weighted by how likely those outcomes are according to the true distribution $P$.

If Cross-Entropy is high, that means that $Q$ assigns low probability to outcomes that are likely under $P$, and because of that, if we use probability distribution $Q$:
- There is more outcomes with low probabilities (high surprise)
- An experiment outcome appears more uncertain ($X$ appears more unpredictable) to us than it truly is

But Cross-Entropy doesn't measure how much more uncertain that would appear, KL Divergence ([[KL Divergence|link]]) does that.
## Assigning high probabilities to unlikely events
Cross-Entropy doesn't tell us too much about a kind of error, when distribution $Q$ assigns a high probability to events which are unlikely according to $P$.

That's because, as we already mentioned, value $-\log(q(x))$ is weighted by $p(x)$, so when $p(x)$ is small, then value $-\log(q(x))$ doesn't contribute a lot to the overall Cross-Entropy value.

Although, when distribution $Q$ assigns to some event higher probability than $P$, then there must be other event, such that $Q$ assigns to it lower probability than $P$. That's because sum of probabilities for all events is constant (equal to 1). 
## Using Cross-Entropy for training models
When distribution $Q$ is defined by our model and we want it to be as similar to the true distribution $P$ as possible, that is we want Cross-Entropy to be as low as possible. 

That means both distributions $P$ and $Q$ assigns high probability to the same events.

#InformationTheory #Mathematics 