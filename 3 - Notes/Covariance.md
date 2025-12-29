Tags: [[_Probability]], [[__Mathematics]]
#Probability #Mathematics 

# Introduction
Covariance tells us whether two random variables $X$ and $Y$ tends to move in one direction or in opposite directions, i.e. it tell us if value of one variable increases or decreases when value of the other variable increases.

To be more precise:
- Positive covariance means that when $X$ is above its means, then $Y$ tends to be above its mean as well (they increase together)
- Negative covariance means that when $X$ is below its means, then $Y$ tends to be below its mean as well (they decrease together)
- Zero covariance means that there is no linear relationship between variables
# Definition
Covariance between $X$ and $Y$ is defined as:
$$
\text{Cov}(X, Y) = \mathbb{E}[(X - \mathbb{E}(X))(Y - \mathbb{E}(Y))]
$$
# Important notes
Covariance has units, that means we can't compare covariance values for different pairs of variables. Also Covariance can equal to any real number. 

Correlation ([[Pearson Correlation|link]]) is the normalized covariance which values are always between -1 and 1, and thanks to that we can compare values of correlation between different pairs of variables.
 