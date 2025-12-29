Tags: [[__Machine_Learning]]

# Introduction
Logistic regression is a model for classification.

It builds on top of linear regression, it also finds parameters for a linear function but output of that linear function is converted such that it always belongs to the range (0, 1) indicating a probability that a given data sample belongs to a given class.
# Related topics
- Classification models - [[Classification models|link]]
- Linear regression - [[Linear Regression|link]]
- Decision threshold - [[Decision - classification threshold|link]]
- Odds - [[Odds|link]]
- Maximum Likelihood Estimation (MLE) - [[Maximum Likelihood Estimation (MLE)|link]]
- Likelihood function - [[Likelihood function|link]]
- Types of probability - [[Types of probability and probability distribution functions|link]]
- Gradient descent - [[Gradient Descent - ML|link]]
- Loss functions - [[Loss functions|link]]
- Cross-Entropy loss functions - [[Cross-Entropy|link]]
# How predictions are made
## Multi-class classification
Logistic regression is built on top of linear regression, it also finds parameters for a linear function:
$$
z_j = w_{j0} + w_{j1} x_1 + ... + w_{jn} x_n = W_j^T x
$$
where
- $W_j = [w_{j0}, ..., w_{jn}]$ are trainable parameters 
- $j = 1, 2, ..., k$ corresponds to different classes
- $x = [x_1, ..., x_n]$ are features in a data sample

Each $z_j$ value (called logit) can be interpreted as indication of how strongly the model believes that given data sample belongs to the $j-th$ class.

Output $z_j$ of that linear function is passed into another function (softmax) which converts it to a number which belongs to the range (0, 1) which represents probability that given sample $x$ belongs to the $j-th$ class:
$$
\large
P(y = j | x) = softmax(z_j) = \frac{e^{z_j}} {\sum_{l=1}^{k} e^{z_l}}
= \frac{e^{W_j^T x}} {\sum_{l=1}^{k} e^{W_l^T x}}
\in (0,1)
$$
Sum of all the probabilities, for every class equals to one:
$$
\sum_{j=1}^k P(y=j|x) = 1
$$
A final prediction $\hat{y}$ is the class with the highest probability:
$$
\hat{y} = \text{arg} \max_j P(y=j | x) \in \{1, 2, ..., k\}
$$
## Binary classification
In case of binary classification, with only two possible classes $y \in \{0, 1\}$, model computes parameters for only one linear function $z = W^T x$ and probability of observing the positive class (y = 1) is given by the following formula using the sigmoid function:
$$
\large
p(x) = P(y = 1 | x) = \text{sigmoid}(z) = \frac{1}{1 + e^{-W^T x}} = \frac{ e^{W^T x} } {1 + e^{W^T x}}
$$
And probability for the negative class ($y = 0$) is:
$$
P(y = 0 | x) = 1 - p(x) = \frac{ 1 } {1 + e^{W^T x}}
$$
Predictions are made using a classification threshold, that is:
$$
\hat{y} = 
\begin{cases}
1,\ \text{if} \ p(x) > \text{classification theshold} \\
0,\ \text{if} \ p(x) <= \text{classification theshold}
\end{cases}
$$
# How to train Logistic Regression
Logistic regression is trained using the Maximum Likelihood Estimation (MLE) method. 

It typically uses gradient descent in order to minimize negative log-likelihood function (i.e. Cross-Entropy loss function) what is equivalent to maximizing likelihood function, i.e. probability of observing the training dataset.

In the MLE method we use the logistic regression's formula for probability of observing a class. In case of a multi-class classification that is:
$$
\large
P(y_i = j | x_i; \theta) = \frac{e^{\theta_j^T x_i}} {\sum_{l=1}^{k} e^{\theta_l^T x_i}}
,\ 
\forall j \in \{1, ..., K\}
$$
So the negative log-likelihood function which will be minimized is:
$$
\large
- l(\theta) 
= - \sum_{i=1}^n \sum_{j=1}^K \mathbb{1} \{y_i = j\} \log( P(y_i = j | x_i; \theta) )
= - \sum_{i=1}^n \sum_{j=1}^K \mathbb{1} \{y_i = j\} \log( \frac{e^{\theta_j^T x_i}} {\sum_{l=1}^{k} e^{\theta_l^T x_i}} )
$$
# Relation between variables
## High level
Logistic regression coefficients can tell us how strong is the relation between each of input variables $x_i$ (that can be both categorical and numerical) and the categorical variable we are trying to predict.

We can convert the equation for $P(y = j | x)$ into an equation for log odds for the class $j$ relative to the reference class $K$:
$$
\text{log-odds}_{j/K} 
= \log( \frac{P(y = j | x)} {P(y = K | x)} ) 
= \beta_{j0} + \beta_{j1} x_1 + ... + \beta_{jn} x_n = \beta_j^T x
$$
where $\beta_{ji} = w_{ji} - c_{i}$ for some parameters $c_{i}$ .

So that means that parameters with bigger absolute values $|w_{ji}|$ has bigger impact on predicted probability of appearing the $j-th$ class. Parameters with positive values increase probability, parameters with negative values decrease it.

More information about why we subtract the $c$ vector, can be found in the [[#Details]] section below in this document.
## Details
We can subtract a vector $c$ from logistic regression's parameters such that parameters $W_K$ for the chosen reference class $K$ equal to zero. 

So we create a new set of model's parameters in the following way:
$$
W_j' = W_j - c,\ \forall j \in {1, ..., K}
$$
where $c$ is such a vector that $W_K' = W_K - c = 0$.

Subtracting such a $c$ helps with interpreting the relation between features $x$ and the target variable $y$, by simplifying an equation for log odds for the class $j$ relative to a reference class:
$$
\text{log-odds}_{j/K} 
= \log( \frac{P(y = j | x)} {P(y = K | x)} ) 
= (W_j - W_K)^T x
= W_j^T x
= \beta_{j0} + \beta_{j1} x_1 + ... + \beta_{jn} x_n = \beta_j^T x
$$

We can perform this subtraction because it doesn't change probabilities:
$$
\large
P(y = j | x; W') 
= \frac{e^{(W_j - c)^T x}} {\sum_{l=1}^{k} e^{(W_l - c)^T x}}
= \frac{e^{-c^T x} e^{W_j^T x}} {e^{-c^T x} \sum_{l=1}^{k} e^{W_l^T x}}
= \frac{e^{W_j^T x}} {\sum_{l=1}^{k} e^{W_l^T x}}
= P(y = j | x; W)
$$

That means that there is an infinite number of possible parameters which gives the same model (the same probabilities / predictions).
# Logistic regression assumptions
The following assumptions must be met in order to use logistic regression effectively:
- **Linearity of log odds:**
	- In case of binary classification, log odds of the event happening are linear in the input features x:
	  $\log(\text{odds}) = \log(\frac{p}{1-p}) = W^T x + b$
	- In case of a multi-class classification, odds of observing the $j$ class relative to any chosen reference class are linear:	  $$\text{odds}_{j/K} = \frac{P(y = j | x)}{P(y = K | x)} = W^T x + b$$ 
- **Independence of observations:** Each observation in the training dataset is independent of others
- **No multicollinearity:** Predictors (x input values) should not be highly correlated with each other
- **Sufficient sample size:** Logistic regression requires enough samples for each combination of predictor values
- **No or minimal outliers:** Extreme values in predictors can heavily influence the log-odds, distorting the fit.