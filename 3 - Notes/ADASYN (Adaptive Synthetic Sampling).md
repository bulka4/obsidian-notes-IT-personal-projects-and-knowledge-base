Tags: [[__Machine_Learning]]

# Introduction
ADASYN (Adaptive Synthetic Sampling) is an oversampling method used when training ML models for classification on an imbalanced dataset ([[Training classification models on an imbalanced dataset|link]]).

It is similar to SMOTE ([[SMOTE (Synthetic Minority Oversampling Technique)|link]]), but it focuses more on difficult-to-learn minority samples.
# How it works
## Identify minority samples
Let the minority class have samples $x = [x_1, \ldots, x_n]$.
## Compute difficulty for each minority sample
For each minority sample $x_i$, find its k nearest neighbors (like in KNN ([[K nearest neighbors (KNN)|link]])) and count how many neighbors belong to the majority class.

Calculate:
$$
r_i = \frac{\text{majority neighbors}}{k}
$$
where:
- High $r_i$ means that the sample $x_i$ is harder to learn (because it is surrounded by majority samples)
- Low $r_i$ means that the sample $x_i$ is easy to learn (because it is surrounded by minority samples)
## Compute the number of synthetic samples per minority sample
ADASYN generates more generates more synthetic points for harder samples:
$$
G_i = \frac{r_i}{\sum_{i}r_i} G
$$
where:
- $G$ - total number of synthetic samples to generate
- $G_i$ - number of synthetic samples for $x_i$ 

So samples which feature vectors are in a dense minority regions (regions densely filled in with feature vectors for the same, minority class ([[Sparsely and densely distributed feature vectors - Visualization|link]])) get fewer new synthetic samples, while harder to learn samples (in less dense regions) get them more.
## Generate synthetic samples
This is done exactly like in SMOTE:
$$
\large
x_{\text{new}} = x_i + \lambda(x_{\text{neighbor}} - x_i), \quad \lambda \in [0,1]
$$
and we repeat it $G_i$ times.
# Pros
- Improves classifier focus on regions in a feature space with hard-to-learn (sparse) feature vectors ([[Sparsely and densely distributed feature vectors - Visualization|link]])
- Can reduce bias toward easy minority regions
- Often better than SMOTE in cases, when boundaries between regions with feature vectors, corresponding to different classes, are complex
# Cons
- Sensitive to noise (outliers get more synthetic points)
- Can still generate unrealistic points if feature space is irregular
- Slightly more complex to implement than SMOTE

#MachineLearning 