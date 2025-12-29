Tags: [[__Machine_Learning]]

# Introduction
Tomek links is an undersampling method for training ML models for classification on an imbalanced dataset ([[Training classification models on an imbalanced dataset|link]]).

It’s more refined than random undersampling ([[Random Undersampling|link]]) because it targets ambiguous samples near class borders (borders between regions with feature vectors for different classes ([[Multiple feature vector groups - Visualization|link]])) instead of removing random majority samples.
# How it works
***1. Identify pairs of nearest neighbors across classes***
For each sample $x_i$​ in the dataset, find its nearest neighbor $x_j$ (the most similar feature vector, like in KNN ([[K nearest neighbors (KNN)|link]])) which belong to a different class.

***2. Define a Tomek Link***
Tomek Link is a pair $(x_i, x_j)$ that satisfies:
- $x_i$ and $x_j$ are nearest neighbors
- They belong to different classes

***3. Remove samples***
There are two strategies:
- Remove the majority class sample in each Tomek Link
- Remove both samples

***4. Result***
It removes samples from majority class which feature vectors are close to other classes.

#MachineLearning 