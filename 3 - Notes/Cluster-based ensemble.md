Tags: [[__Machine_Learning]]
#MachineLearning 

# Introduction
A Cluster-based ensemble technique is used to train ML models for classification on an imbalanced dataset ([[Training classification models on an imbalanced dataset|link]]).

It is similar to the EasyEnsemble method ([[EasyEnsemble|link]]), we also split the original dataset into multiple, smaller, balanced datasets, but instead of randomly choosing samples for each new dataset, we perform clustering.
# How it works
It works like that:
- Divide the majority classes into L distinct clusters. 
- Train L predictors, where each predictor is trained on:
	- Data samples from only one of the clusters
	- All of the data from the minority class
- To make the final prediction:
	- Each model makes a prediction
	- We take an average of all predictions