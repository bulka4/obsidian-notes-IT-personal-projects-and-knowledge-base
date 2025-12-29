Tags: [[__Machine_Learning]]

# Introduction
PCA (Principal Component Analysis) is a technique for reducing dimensionality of a dataset ([[Dimensionality reduction|link]]), which reduces number of features by creating new ones, called principal components, which are:
- linear combinations of the original features
- uncorrelated
- ordered by how much variance they explain
# How it works
Let's assume, that we have a dataset like described here - [[Dataset of observations of random variables X, Y - Variables per feature and target variable|link]], that is $n$ observations of feature and target random variables $X_i$ and $Y$, where:
- $X_i$ - Random variable corresponding to the $i$-th feature
- $x_{ij}$ - The $j$-th observation of a random variable $X_i$ . So that is a value of the $i$-th feature from the $j$-th data sample.

PCA is performed in the following way:

***1. Create covariance matrix***
We need to calculate the mean of each feature and use it to calculate covariance matrix $\Sigma$ ([[Covariance matrix|link]]). We approximate expected value with the mean, so covariance formula becomes:
$$
\large
\text{cov}(X_i, X_j) = \frac{1}{n-1} \sum_{k=1}^n (x_{ik} - \bar{x_i}) (x_{jk} - \bar{x_j})
$$
where:
- $\large \bar{x_i} = \frac{1}{n} \sum_{k=1}^n x_{ik}$ - Mean of observations of the random variable $X_i$ 

***2. Find eigenvectors and eigenvalues of the covariance matrix***
Find eigenvectors $v_i$ ([[Eigenvectors|link]]), such that $||v_i|| = 1$, and corresponding eigenvalues $\lambda_i$ of the covariance matrix $\Sigma$. So those are such vectors, that:
$$
\large
\Sigma v_i = \lambda_i v_i, \quad \text{where } ||v_i|| = 1
$$

***3. Sort components by eigenvalues***
Keep the top k components $v_i$ (eigenvectors with the highest eigenvalues).

Each component (eigenvector) is used to create new features, by multiplying it by old features:
$$
\large
PC_i = v_i^T x_i = \sum_{j=1}^d v_{ij} x_{ij}
$$
where $x_i$ are observations of a random variable $X_i$ from our dataset.
# Interpretation - why it works like that
In PCA, we want to create new features, called principal components noted as $PC_i$ , which are a linear combination of the current features $X_i$:
$$
PC_i = v_i^T X_i
$$
for some vector $v$. This is our assumption / choice, that we want new variables of this form.

We want the variance for those new features:
$$
\text{Var}(PC_i) = \text{Var}(v_i^T X_i)
$$
to be as high as possible. Features with a higher variance might help a model to detect what is the relation between that feature $X_i$ and the target variable $Y$ as described here - [[Feature selection with a variance threshold]] in the 'Interpretation' section.

From the definition of variance, we have:
$$
\large
\text{Var}(v_i^T X_i) = v_i^T \Sigma v_i
$$
Rayleigh Quotient Theorem tells us, that the biggest value of this formula $\large v_i^T \Sigma v_i$ is for the eigenvector $v_i$ w.r.t. to $\Sigma$ with the highest corresponding eigenvalue $\lambda_i$ . 

From the definition, eigenvector satisfies:
$$
\large
\Sigma v_i = \lambda_i v_i
$$
So the variance becomes:
$$
\large
\text{Var}(v_i^T X_i) = v_i^T \Sigma v_i = 
v_i^T (\lambda_i v_i) = \lambda_i (v_i^T v_i) = \lambda_i ||v_i||^2
$$
In PCA we require vectors $v_i$ to have length equal to one $||v_i|| = 1$, so that simplifies to:
$$
\large
\text{Var}(v_i^T X_i) = \lambda_i
$$
So for k PCA components $PC_i$ we choose k eigenvectors $v_i$ with the biggest corresponding eigenvalue $\lambda_i$ , because that gives the biggest variance for the new features.

Value $v_i^T X_i$ is so called projection of $X_i$ onto $v_i$ .
# Cons of PCA
- Loss of interpretability - We can't interpret new features
- PCA is linear - It can't capture non-linear dependencies between features
- Sensitive to scaling - If features are not standardized, PCA can be dominated by features with higher values
- Sensitive to outliers - Outliers can significantly affect how the covariance matrix look like
- May discard useful variance - Usually higher variance gives us more information but not always. Sometimes target variable depends of features with a lower variance.
- PCA doesn't consider the target variable - Chosen components maximizes variance of features but not how useful they are for predicting target variable $Y$. Sometimes, features with high variance are not the best predictors of $Y$.

#MachineLearning 