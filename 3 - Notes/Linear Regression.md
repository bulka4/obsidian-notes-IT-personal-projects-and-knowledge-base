Tags: [[__Machine_Learning]]

# Introduction
Linear Regression is a model for regression. It tries to model relationship between:
- Input (features) - $X = [x_1, ..., x_n]$
- Output (target) - $Y$
by finding a straight line (linear function) that best fits data.

Predictions are made using a linear function:
$$
\hat{y} = w_0 + w_1 * x_1 + ... + w_n * x_n = Xw
$$
for input $X = [x_1, ..., x_n]$.

The $w = [w_1, ..., w_n]$ vector consist of trainable parameters (weights) we are trying to find.
# Benefits
- Easy to interpret - Coefficients show what impact each feature has on the target variable
- Fast to train and make predictions
- Requires relatively little data
- Can extrapolate ([[Machine Learning - Extrapolation|link]])
- Works well when relationship between the target variable and features is linear
- With regularization ([[Regularization|link]]) handles well high-dimensional datasets and irrelevant features - Irrelevant features contribute a little to the prediction while relevant ones contribute a lot.
# Drawbacks
- Assumes a linear relationship between features and target, constant variance, independency of samples
- Sensitive to outliers
- Might not learn complex / nonlinear relationships between the target variable and features
# How linear regression works
Linear regression finds such a weights $w = [w_1, ..., w_n]$ that minimizes a chosen loss function (more information about loss functions can be found [[Loss functions|here]]).

There are two methods of calculating weights that minimizes an error:

***1. Normal equation - Analytical (exact) solution***
Weights are calculated using the formula:
$$
w = (X^TX)^{-1} X^T y
$$
where $X$ and $y$ are values from the training dataset. 

$X$ is a matrix where each row represents a data sample and each column represents a feature, and $y$ is a vector with target values we are trying to predict.

The i-th record from the $X$ matrix corresponds to the i-th value of the vector $y$.

***2. Gradient descent***
It is an iterative, approximated solution. More information about it can be found [[Gradient Descent - ML|here]]
# Linear regression assumptions
There are some assumptions made when using linear regression. If those conditions are not satisfied, linear regression will not give good results.

Those assumptions are:
- **Linearity** — relationship between X and y is linear
- **Independence** — observations (data samples) are independent - covariance of errors for different samples is equal to 0 (More about errors in the [[#Error]] section below)
- **Homoscedasticity** — variance of errors is constant
- **Normality** — errors are normally distributed
- **No multicollinearity** — features aren’t strongly correlated
## Error
Errors represents a noise or randomness in the true data-generating process (the 'true' linear function which generated data). Those are theoretical values (or rather a function) which we assume that exists.

We assume that:
$$
y_i = \hat{y}_i + \epsilon_i
$$
where:
- $y_i$ - The real value for the i-th data sample
- $\hat{y}_i$ - Prediction of the real value for the i-th data sample made by the 'true' linear function - the true function that generated data without error
- $\epsilon_i$ - Error which appears together with the 'true' linear function for the i-th data sample
# Relation between variables
Logistic regression coefficients can tell us how strong is the relation between each of input variables $x_i$ (that can be both categorical and numerical) and the continuous variable we are trying to predict.