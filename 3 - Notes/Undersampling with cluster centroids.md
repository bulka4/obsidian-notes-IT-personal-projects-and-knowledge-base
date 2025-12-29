Tags: [[__Machine_Learning]]

# Introduction
Undersampling with cluster centroids is an undersampling method for training ML models for classification on an imbalanced dataset ([[Training classification models on an imbalanced dataset|link]]).

It summarizes the majority class using cluster centroids ([[Cluster centroids|link]]).
# How it works
Take all the samples which belong to the majority class and cluster them using for example K-Means ([[K means clustering|link]]) to group them into $k$ clusters.

All the samples from each cluster is then replaced with their cluster centroids.

#MachineLearning 