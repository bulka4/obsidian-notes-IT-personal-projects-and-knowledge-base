Tags: [[__Machine_Learning]]

# Introduction
Random Undersampling is a method for training ML models for classification on an imbalanced dataset ([[Training classification models on an imbalanced dataset|link]]).

It is done by randomly selecting a subset of data samples which belong to the majority class, with a similar size to the group of samples for the minority class, and dropping the rest of the samples.
# Pros
- Simple to implement
- Reduces training time
- Works well if the majority class has a lot of redundant or similar samples
# Cons
- We might loose useful information from the dropped samples
- Results might depend on which samples we will drop
- We might end up with too little data samples in total and model performance will be poor

#MachineLearning 