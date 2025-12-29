Tags: [[__Machine_Learning]]

# Introduction
SMOTE (Synthetic Minority Oversampling Technique) is a technique for dealing with an imbalanced dataset when training ML models for classification ([[Training classification models on an imbalanced dataset|link]]).

It creates new, synthetic data samples, which have feature values between other, similar samples.
# How it works
Pick one data sample ([[Features and target variables|link]]) which belongs to the minority class:
$$
x = [x_1, \ldots, x_n] \text{ - vector with features}
$$
Find k nearest neighbors of that feature vector (the most similar vectors, like in KNN ([[K nearest neighbors (KNN)|link]])) and choose one of them:
$$
\large
x_{\text{neighbor}}
$$
Compute the difference between those vectors:
$$
\text{diff} = x_{\text{neighbor}} - x
$$
and multiply by a random number between 0 and 1 (with a uniform distribution):
$$
\lambda \cdot \text{diff}, \quad \lambda \sim U(0,1)
$$
and use it to create a new, synthetic data sample:
$$
\large
x_{\text{new}} = x + \lambda(x_{\text{neighbor}} - x)
$$
# Pros
## Reduced overfitting
Random Oversampling ([[Random Oversampling|link]]) creates duplicated, identical data samples, so model can memorize them what causes overfitting ([[Overfitting and generalization|link]]).

SMOTE creates new samples, slightly different than the existing ones what improves generalization.
## Minority regions become denser
Synthetic samples fill gaps in sparse minority regions - regions in a feature space ([[Feature space|link]]) with sparsely distributed feature vectors corresponding to the minority class, like shown here - [[Sparsely and densely distributed feature vectors - Visualization|link]].

So minority regions become denser, data samples are less isolated what helps a model to learn detecting which samples belong to that class.
# Cons
## Can create unrealistic data samples
SMOTE interpolates linearly between neighbors. If the relationship between features is non-linear, then SMOTE might generate unrealistic data points.
## Can cause class overlap
If feature vectors corresponding to the minority class are close to feature vectors corresponding to the majority class (features are similar) like illustrated here - [[Multiple feature vector groups - Visualization|link]], SMOTE may generate new feature vectors in a region, where we have feature vectors which belong to other class, increasing overlap and hurting performance.
## Doesn't perform well in high-dimensional datasets
In high-dimensional datasets, nearest neighbors become less meaningful.
# When SMOTE works best
Use SMOTE if:
- Minority class is small but well-separated (feature vectors are far away from feature vectors of other classes)
- Most minority samples are informative (not noise)
- Feature relationships are roughly linear or smooth

Avoid or be cautious when:
- The minority class contains many outliers ([[Training datasets for ML models - Outliers|link]])
- The boundary between regions with feature vectors for different classes is highly complex or nonlinear
- You have very high-dimensional data (text vectors, images)
- The minority class is extremely small

#MachineLearning 