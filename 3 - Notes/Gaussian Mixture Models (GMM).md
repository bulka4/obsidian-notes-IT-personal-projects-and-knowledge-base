Tags: [[__Machine_Learning]]

# Introduction
Gaussian Mixture Models (GMM) is a technique for detecting anomalies ([[Anomaly Detection models|link]]). It assumes that data is generated from multiple Gaussian (normal) distributions, each representing a cluster.

It fits a Gaussian distribution to each cluster which form together a mixture distribution which can be used to detect outliers (anomalies).
# How it works
We assume K Gaussian distributions:
 - We choose it or we can use for example BIC to find it. 
 - One distribution is assigned to one group of samples in our dataset

Then we estimate parameters of each distribution using the Expectation-Maximization (EM) algorithm:
- E-step: estimate how likely each point belongs to each Gaussian
- M-step: update the Gaussian parameters based on those assignments

For each point, GMM gives:
- probability of belonging to each cluster
- overall probability density

This makes GMM a soft clustering model (points belong partially to multiple clusters, for each cluster there is some probability that the point belongs to it).

We can flag anomalies as points with low probability under the mixture model.
# Multiple features
If our dataset consists of multiple features, then each Gaussian distribution is multivariate, that means it has:
- A mean vector (one mean per feature)
- A covariance matrix - Variance per feature plus correlations between features
# Pros
It is better than Z-score ([[Z-Score - Standard Deviation|link]]) because:
- allows multiple clusters
- handles skewed or complex shapes of variable distributions
- models correlations between features via covariance

# When it works well
- We have multiple clusters in a dataset
- There are multiple features
- Variables are continuous
# When it doesn't work well
- Too many dimensions (covariance matrices get complex)
- Clusters that are non-Gaussian (e.g., spirals)
- Large outliers without preprocessing

#MachineLearning 