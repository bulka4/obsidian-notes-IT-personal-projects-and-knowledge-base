Tags: [[__Machine_Learning]]

# Introduction
This document describes how to train models for classification on an imbalanced dataset ([[Training ML models on an imbalanced dataset|link]]).
# Data-level methods
## Oversampling minority class
Increase number of samples for the minority class using methods like:
- Random Oversampling: ([[Random Oversampling|link]]) 
	- Duplicate minority samples.
- SMOTE (Synthetic Minority Oversampling Technique): ([[SMOTE (Synthetic Minority Oversampling Technique)|link]])  
	- Creates synthetic minority samples by interpolating between existing ones.
- ADASYN: ([[ADASYN (Adaptive Synthetic Sampling)|link]])
	- Like SMOTE, but focuses more on difficult-to-learn minority samples.
Pros:
- Simple and often effective
- Prevents loss of information
Cons:
- Random oversampling can cause overfitting
- Synthetic oversampling may introduce noise
## Undersampling the majority class
Reduce the number of samples for the majority class.

Methods:
- Random Undersampling ([[Random Undersampling|link]])
- Tomek links: ([[Tomek links|link]]) 
	- Remove ambiguous samples near class boundaries.
- Cluster Centroids: ([[Undersampling with cluster centroids|link]]) 
	- Replace clusters of majority samples with their centroids.
Pros:
- Fast, reduces training time
- Useful for huge datasets
Cons:
- Risk of losing important information
# Algorithm-level methods
These modify how the model learns rather than modifying the dataset.
- Class Weights / Cost-Sensitive Learning - [[Class Weights - Cost-Sensitive Learning|link]]
	- Assign higher importance (weight) to mistakes on the minority class.
	- **Effect:**  Model tries harder to correctly classify the minority class.
- Focal Loss (deep learning) - [[Focal loss|link]]
	- Designed for highly imbalanced datasets (e.g., object detection).  
	- It down-weights easy examples and focuses more on hard ones.
## Anomaly Detection Models
If the minority class is extremely rare (<1%), treat the problem as anomaly detection instead of classification. More information can be found here - [[Anomaly Detection models]].
## Balanced Ensemble Methods
Those are methods, which divide the dataset into multiple, smaller, balanced datasets and train different models on each one. Then all the models are used together to make predictions.

Balanced ensemble Methods include:
- EasyEnsemble - [[EasyEnsemble|link]]
- Balanced Random Forest - [[Balanced Random Forest|link]]

#MachineLearning 