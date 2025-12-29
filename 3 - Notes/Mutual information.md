Tags: [[_Information_theory]], [[__Mathematics]]

# Introduction
Mutual information (MI) is related to uncertainty of an experiment outcome and surprise measure. We can learn more about them here - [[Experiment outcome uncertainty and average surprise measures]].

Mutual information can be interpreted as a formula which measures:
- How much knowing one variable tells us about another
- A reduction in uncertainty or average surprise of a random variable $X$ after seeing $Y$ 
- How much correlated are two variables

Mutual information is always greater or equal to zero and higher values indicates stronger relation between variables.

If mutual information for $X$ and $Y$ is high, that means that $X$ is a useful feature for predicting target variable $Y$.
# Definition
Mutual information is defined as:
$$
\large
I(X;Y) = \mathbb{E}_{P_{X, Y}} 
(\log( \frac{p_{X, Y}(X, Y)} {p_X(X) p_Y(Y)}))
$$
where:
- $p_{X, Y}$ - Joint probability distribution function of $X, Y$ 
- $p_X$ - Marginal probability distribution function of $X$ 
## Discrete random variables
For discrete random variables $X, Y$, using the fact how expected value looks like for discrete random variables ([[Expected value|link]]), Mutual information equation looks like:
$$
\large
I(X;Y) = \sum_{x,y} p_{X, Y}(x,y)\log(\frac{p_{X, Y}(x, y)}{p_X(x)p_Y(y)})
$$
## Continuous random variables
For continuous random variables $X, Y$, using the fact how expected value looks like for continuous random variables ([[Expected value|link]]), Mutual information in defined as:
$$
I(X;Y) = \int p_{X, Y}(x,y) \log(\frac{p_{X, Y}(x, y)}{p_X(x)p_Y(y)})\ dx\ dy
$$
# Relation to KL Divergence
Mutual information formula can be expressed using the KL Divergence ([[KL Divergence|link]]):
$$
I(X;Y) = D_{KL}(p_{X, Y}(x,y) \mid\mid p_X(x)p_Y(y))
$$
Using the interpretation of KL Divergence, we can interpret that as a difference between $p_{X, Y}$ and $p_X \cdot p_Y$ .

If $X, Y$ are independent, then $p_{X, Y} = p_X \cdot p_Y$, so MI measures how far $X$ and $Y$ are from being independent.

Also, KL Divergence is related to Cross-Entropy and Entropy. Additional, more precise interpretation, related to those concepts, can be found in the next section 'Relation to Cross-Entropy'.
# Relation to Cross-Entropy
As already mentioned, Mutual information is related to KL Divergence, and KL Divergence is related to the Cross-Entropy ([[Cross-Entropy|link]]) as explained here - [[Relation between KL Divergence and Cross-Entropy and Entropy|link]]:
$$
D_{KL}(p || q) = H(p, q) - H(p)
$$
where:
- $H(p)$ is Entropy - How unpredictable pair $(X, Y)$ truly is according to its true distribution $p = p_{X, Y}$ 
- $H(p, q)$ is Cross-Entropy - How unpredictable the pair $(X, Y)$ appears to us if we use modeled distribution $q$ instead of the true distribution $p = p_{X, Y}$ 
If we use as the modeled distribution $q = p_X \cdot p_Y$, we are assuming that $X$ and $Y$ are independent.

So MI measures how how much more unpredictable the pair $(X, Y)$ would appear to us than it truly is, if we falsely assume that $X$ and $Y$ are independent.

Or we can also describe it as how much more surprised we would be when observing realizations of the pair $(X, Y)$ if we use $q = p_X \cdot p_Y$ instead of $p = p_{X, Y}$.
# Relation to Entropy
Mutual information can be also expressed using only the Entropy ([[Entropy|link]]):
$$
\begin{align}
 & I(X;Y) = H(X) - H(X \mid Y) \\
 & I(X;Y) = H(Y) - H(Y \mid X) \\
\end{align}
$$
Using the Entropy interpretation:
- $H(X)$ - How unpredictable $X$ is
- $H(X \mid Y)$ - How unpredictable $X$ is given Y
that gives us an interpretation of MI, that it is a reduced uncertainty of $X$ after seeing $Y$ 
# Relation to correlation
Correlation ([[Pearson Correlation|link]]) measure linear dependence, while MI measure any dependence.

For example, if $X \sim \text{Uniform}(-1,1)$ and $Y = X^2$, then:
- $\text{Corr}(X, Y) = 0$ 
- $I(X; Y) > 0$ 
# Properties
## Non-negative
For any random variables $X, Y$: $I(X;Y) \ge 0$ 
## Perfect correlation
If $Y = X$, then $I(X;Y) = H(X)$ 

All of $X$ uncertainty disappears when we know $Y$/
## Independent variables
If $X, Y$ are independent, then $I(X;Y) = 0$, because $p(x, y) = p(x)p(y)$ 

#InformationTheory #Mathematics 