Tags: [[__Machine_Learning]]

# Introduction
Usually, in case of classification, for a given data sample, machine learning model output is a probability distribution over classes, that is a vector:
$$
\{p_i\}_{i=1}^K
$$
where each element corresponds to a specific class and represents a probability that this is a true class for a given data sample.

So $p_i$ is a probability that the $i$-th class is a true class for a given data sample.

So in this example, in total we have $K$ classes and probabilities for all of them sum up to 1:
$$
\sum_{i=1}^K p_i = 1
$$
# Model's output as class probabilities
Let's assume, that:
- Machine learning model is a parametric function $f_\theta:\ \mathcal{X} \rightarrow \mathcal{Y}$ ([[What is a Machine Learning model|link]])
- Model is trained using a dataset $D = \{ (x_i, y_i) \}_{i=1}^n$, where each sample $(x_i, y_i)$ is a realization of random variables $X_i$ and $Y_i$ ($X_i$ - features, $Y_i$ - target variable) ([[Dataset of observations of random variables X, Y - Variables per sample, feature and target variable|link]]).

Usually (but not always), in case of classification, for a given data sample $x_i$, machine learning model output $f_\theta(x_i)$ is a probability distribution over classes, that is a vector:
$$
f_\theta(x_i) = \{P(Y_i = y_j \mid X_i = x_i; \theta)\}_{j=1}^K
$$
where:
- $y_j,\ j = 1, ..., K$ - Represents all the classes
- $P(Y_i = y_j \mid X_i = x_i; \theta)$ - Probability that the $i$-th data sample (input $x_i$) belongs to the class $y_j$ under parameters $\theta$ 
- $\sum_{j=1}^K P(Y_i = y_j \mid X_i = x_i; \theta) = 1$ - Sum of probabilities for all the classes equals 1
# Examples
For example, in case of a multi-class classification, the probability for the $j$-th class can be given with the following formula using softmax function:
$$
\large
f_{\theta, j}(x_i) = P(Y_i = y_j \mid X_i = x_i; \theta) 
= softmax(\theta_j^T x_i)
= \frac{e^{\theta_j^T x_i}} {\sum_{l=1}^{k} e^{\theta_l^T x_i}} \in (0,1)
$$
And in case of a binary classification, when $Y_i$ has only two possible values 0 and 1, it is enough for the model to output a single value:
$$
\large
p(x_i) = P(Y_i = 1 \mid X_i = x_i; \theta)  = \text{sigmoid}(\theta^T x_i) = \frac{1}{1 + e^{-\theta^T x_i}} = \frac{ e^{\theta^T x_i} } {1 + e^{\theta^T x_i}}
$$
and then, probability for the second class is:
$$
P(Y_i = 0 \mid X_i = x_i; \theta) = 1 - p(x_i)
$$
# Probability distribution function
Probabilities from model's output can be used to define the probability distribution function.

More information about it can be found here:
- [[Probability distribution - Introduction]]
- [[Conditional probability distribution (density, mass) function]]
- [[Conditional probability distribution function - Discrete random variables]]

For a multi-class classification, the probability distribution function can be define like this:
$$
\Large
\begin{align}
 & p_{Y \mid X}(y \mid x) = \sum_{i=1}^n \mathbb{1} \{y = y_i\} P(Y = y_i \mid X = x) \\
 & p_{Y \mid X}(y \mid x) = \prod_{i=1}^n P(Y = y_i \mid X = x)^{ \mathbb{1} \{y = y_i\} }
\end{align}
$$
where:
- $Y, X$ - Random variables representing a single data sample 
- $y$ - Function argument
- $x$ - Fixed value for the condition. For different values of $x$ we receive different probability distribution functions $p_{Y \mid X}(y \mid x)$ 

And for a binary classification, when $Y$ has only two possible values 0 and 1, we can define the probability distribution function like this:
$$
\Large
p_{Y \mid X}(y \mid x) = p^{y} (1 - p)^{1 - y},\ y \in \{0, 1\}
$$
where $p = P(Y = 1 \mid X = x)$.

Those formulas work because they satisfy the condition:
$$
p_{Y \mid X}(y_i \mid x) = P(Y = y_i \mid X = x),\ \forall i = 1, \ldots, K
$$
where $y_i,\ i = 1, \ldots, K$ represents all possible classes.
# Related topics
1. [[What is a Machine Learning model]]
2. [[Dataset of observations of random variables X, Y - Variables per sample, feature and target variable]]
3. [[Probability distribution - Introduction]]
4. [[Conditional probability distribution (density, mass) function]]
5. [[Conditional probability distribution function - Discrete random variables]]

#MachineLearning 