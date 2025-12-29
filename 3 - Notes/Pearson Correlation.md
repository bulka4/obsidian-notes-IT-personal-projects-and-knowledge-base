Tags: [[_Probability]], [[__Mathematics]]
#Probability #Mathematics 

# Introduction
Pearson Correlation measures how much change in value of one random variable $X$ impacts a value of the other random variable $Y$. It measure a linear relation between $X$ and $Y$.

It is a value between -1 and 1, with the following interpretation:
- Correlation close to 1 means that when value of $X$ increases, then value of $Y$ usually also increases by a proportional value
- Correlation close to -1 means that when value of $X$ increases, then value of $Y$ usually decreases by a proportional value
- Correlation equal to 0 means that there is no linear relation between $X$ and $Y$ 

There are different types of correlation which measures different types of relation between random variables.
# Definition
Pearson Correlation measures a linear dependence between two variables. It is defined as:
$$
\text{Corr}(X, Y) = \rho_{X, Y} = \frac{\text{Cov}(X, Y)}{\sigma_X \sigma_Y}
$$
where:
- $\text{Cov}(X, Y)$ - Covariance between $X$ and $Y$ ([[Covariance|link]])
- $\sigma_X$ - Standard deviation of $X$ ([[Standard deviation|link]])
# Important points
## 1. Correlation does NOT imply causation
Just because X and Y move together does not mean X causes Y.  There may be a third variable or coincidence.
## 2. Correlation measures only linear dependence
Two variables may be strongly related but non-linearly, for example:
$$
Y=X^2
$$
Correlation is almost 0 — yet Y completely depends on X.
## 3. Sensitive to outliers
One extreme data point can dramatically change correlations.
## 4. Symmetric
$\text{Corr}(X, Y) = \text{Corr}(Y, X)$ 
## 5. Relation to covariance
Correlation ([[Pearson Correlation|link]]) is the normalized covariance which values are always between -1 and 1, and thanks to that we can compare values of correlation between different pairs of variables.

Covariance ([[Covariance|link]]), on the other hand, has units, that means we can't compare covariance values for different pairs of variables. Also Covariance can equal to any real number. 
 