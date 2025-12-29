Tags: [[__Machine_Learning]]

# Introduction
Overfitting is a situation when model performs well on the training dataset ([[Train - test split of a dataset|link]]) but poorly on new data samples, which model didn't see during training.

That means that model probably has learnt only the noise and irrelevant patterns appearing in the training dataset rather than general trends and relations.

This usually happens, when:
- Model is too complex (too many parameters relative to the number of samples in the dataset)
- Some of the model parameters are much bigger than others (so model relies much more on a subset of features, which correspond to those big parameters)
- Models learns irrelevant patterns (noise) in the data
- There is too little data samples in the training dataset

Generalization is model's ability to perform well on new data samples, which model has never seen before. So model generalizes well if there is no overfitting.

#MachineLearning 