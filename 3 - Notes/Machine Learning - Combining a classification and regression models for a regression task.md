Tags: [[__Machine_Learning]]
#MachineLearning 

# Introduction
We can combine a classification and regression models for a regression task such that:
- We cluster a continuous target variable such that each cluster contains a specific range of values. For example:
	- We want to predict a revenue 
	- One cluster contains samples with a revenue range 10k - 20k
	- Second cluster contains samples with a revenue range 20k - 30k
	- etc
- A classification model predicts a target range cluster
- Then, a regression model takes as an input the output of the classification model (a target range cluster) and based on that predicts an exact value of the target variable

There are two options how to train a regression model in that case:
- Train one model for all the target range clusters
- Train a separate model per each target range cluster