Tags: [[_My_projects]] [[__Machine_Learning]]
#MyProjects #MachineLearning 

# Introduction
IN this project we we try to predict whether a user will click an add.
# Code repository
Repository with project's code - [github.com](https://github.com/bulka4/add_click_prediction).
# Data preparation
To prepare data for training, we:
- Remove outliers
- Encode categorical variables - using the mean encoding ([[Encoding categorical variables - Target - mean encoding|link]])
- Use standarization to scale variables ([[Standarization|link]])
# Model
We test here different models using `sklearn`:
- Logistic regression ([[Logistic Regression|link]])
- KNN ([[K nearest neighbors (KNN)|link]])
- Random forest ([[Random Forest|link]])
- Neural network (using the `Sequential` function, dense layers plus dropout)
## Testing model parameters
We use the `GridSearchCV` function from `sklearn` to test models with different parameters.
## Regularization
We use the l1 penalty ([[L1 Regularization (Lasso)|link]]) and elastic net ([[Elastic Net Regularization|link]]) for regularization during model training.