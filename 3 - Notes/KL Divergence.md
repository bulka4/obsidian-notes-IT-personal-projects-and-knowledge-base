Tags: [[_Information_theory]], [[__Mathematics]]

# Introduction
KL Divergence is related to uncertainty of an experiment outcome and surprise measure. We can learn more about them here - [[Experiment outcome uncertainty and average surprise measures]].

The KL Divergence is a formula for calculating the divergence (difference) between two probability distribution functions ([[Probability distribution (density, mass) function|link]]) $P$ and $Q$.

Part of this formula is the Cross-Entropy formula ([[Cross-Entropy|link]]).

It measures how more surprised, on average, we are by experiment outcomes when using probability distribution $Q$, weighted by how likely are those outcomes according to the probability distribution $P$.

Low KL Divergence indicates that both distributions assign high probabilities to the same events, but it doesn't tell us too much about situations, when distribution $Q$ assigns high probabilities to events which are unlikely according to $P$.

KL Divergence can be used for training statistical models. We find such parameters for a model, which minimizes Cross-Entropy, thus minimizes KL Divergence.

We minimize KL Divergence because lower value indicates that probability distribution defined by our model is similar to the true distribution of random variables which generated given dataset.
# Formula
Let's assume, that:
- $X, Y$ - Random variables ([[Random variable|link]])
- $p, q$ - Conditional probability distribution functions of $Y \mid X = x$ (fixed condition $x$) ([[Conditional probability distribution (density, mass) function|link]])
- $p$ and $q$ corresponds to probability distributions $P$ and $Q$ 

The KL Divergence is defined as:
$$
\large
D_{KL}(p \lVert q) = \mathbb{E}_{P(Y \mid X = x)} 
(\log( \frac{p(Y \mid x)} {q(Y \mid x)}))
$$
where:
- $\mathbb{E}_{P(Y \mid X = x)}$ is expected value ([[Expected value|link]]) with respect to the conditional probability distribution $\large P_{Y \mid X = x}$ 

Analogical formula can be used for non-conditional probabilities.
# Relation to Cross-Entropy and Entropy
[[Relation between KL Divergence and Cross-Entropy and Entropy]]
# Using KL Divergence for training models
[[Using KL Divergence for training models]]
# Interpretation
***Recollection***
Let's remind, that KL Divergence formula is:
$$
\large
D_{KL}(p \lVert q) = \mathbb{E}_{P(Y \mid X = x)} 
(\log( \frac{p(Y \mid x)} {q(Y \mid x)})) = 
\int_\mathbb{R} p(y \mid x) 
\log(\frac{ p(y \mid x) } { q(y \mid x) }) dy
$$
where $\large p(y \mid x) = p_{Y \mid X}(y \mid x)$ is a conditional probability distribution function, where $x$ is fixed and only $y$ is an argument.
## Uncertainty and average surprise
Interpretation of KL Divergence is related to uncertainty of an experiment outcome and its average surprise. We can learn more about those concepts from here - [[Experiment outcome uncertainty and average surprise measures]].
## Extra surprise measure
The fraction $\large \log(\frac{p(y \mid x)}{q(y \mid x)})$ measures how much extra 'surprise' we gain relatively to $P$ by using the distribution $Q$ because:
$$
\large 
\begin{align}
& \log(\frac{p(y \mid x)}{q(y \mid x)}) = \log(p(x)) - \log(q(x)) = -\log(q(x)) -(-\log(p(x))) \\
& \quad = \text{(surprise according to Q)} - \text{(surprise according to P)}
\end{align}
$$
## Weighting a surprise
That amount of extra 'surprise' is weighted by the value $p(y \mid x)$, so that means that when value $p(y \mid x)$ is high, then the extra 'surprise' $\large \log(\frac{p(y \mid x)}{q(y \mid x)})$ contributes more to the entire KL Divergence value.

So KL Divergence is low, when the extra 'surprise' $\large \log(\frac{p(y \mid x)}{q(y \mid x)})$ is low for such values $y$, for which  $p(y \mid x)$ is high.

In other words, KL Divergence is low, if outcomes (realizations of $Y$) which are likely according to the distribution $P$, are also likely according to the distribution $Q$.
## What KL Divergence measures
We usually use as $Q$ probability distribution defined by a statistical model and $P$ indicates the true probability distribution.

KL Divergence measures how much more 'surprised' we are on average by experiment outcomes (observations of $Y$) when we use distribution $Q$ instead of $P$, weighted by how likely those outcomes are according to the true distribution $P$.

If KL Divergence is high, that means that $Q$ assigns low probability to outcomes that are likely under $P$, and because of that, if we use probability distribution $Q$:
- There is more outcomes with low probabilities (high surprise)
- An experiment outcome appears more uncertain ($X$ appears more unpredictable) to us than it truly is

And KL Divergence measures how big is that increase of uncertainty.
## Assigning high probabilities to unlikely events
KL Divergence doesn't tell us too much about a kind of error, when distribution $Q$ assigns a high probability to events which are unlikely according to $P$.

That's because, as we already mentioned, value $\large \log(\frac{p(y \mid x)}{q(y \mid x)})$ is weighted by $p(x)$, so when $p(x)$ is small, then value $\large \log(\frac{p(y \mid x)}{q(y \mid x)})$ doesn't contribute a lot to the overall KL Divergence value.

Although, when distribution $Q$ assigns to some event higher probability than $P$, then there must be other event, such that $Q$ assigns to it lower probability than $P$. That's because sum of probabilities for all events is constant (equal to 1).

#InformationTheory #Mathematics 