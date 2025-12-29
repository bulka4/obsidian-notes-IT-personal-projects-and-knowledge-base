Tags: [[__Machine_Learning]]

# Introduction
EasyEnsemble is a balanced ensemble method used to train ML models for classification on an imbalanced dataset ([[Training classification models on an imbalanced dataset|link]]).

It builds multiple classifiers, each trained on a different balanced subset of the data.

It is similar to Balanced Random Forest ([[Balanced Random Forest|link]]) but designed mainly for boosting models (especially AdaBoost ([[AdaBoost|link]])), not random forests.
# How it works
- Keep all minority-class samples as they are
- For each ensemble member (i.e. for each model we want to train):
    - Randomly select samples from the majority class
	    - Pick a similar number of samples as for the minority class
    - Combine this majority subset with the full minority class, that gives us a balanced dataset
- Train a classifier (usually AdaBoost) on this balanced dataset
- Repeat steps 2–3 many times (e.g., 10–50 balanced datasets)
- To make predictions, combine predictions from all models (usually by averaging or weighted voting)
# Pros
- Uses more majority-class information than random undersampling
- Uses all minority samples every time
- Works well with complex boundaries (boundaries between regions with feature vectors for data samples of different classes ([[Multiple feature vector groups - Visualization|link]]))
- Less prone to overfitting than SMOTE-based ([[SMOTE (Synthetic Minority Oversampling Technique)|link]]) approaches
# Cons
- Multiple models → higher computational cost

#MachineLearning 