Tags: [[__Machine_Learning]]
#MachineLearning 

# Introduction
Evaluating a model means calculating a metric which shows how effective model is on a new data which this model never saw during training.
# Preparing data for evaluation
In order to evaluate a model, we need to prepare data for it. Techniques for that include:
- Train-test split - Use one dataset for training a model and a separate dataset for testing it ([[Train - test split of a dataset|link]])
- Cross Validation - create multiple separate sets of training and testing datasets ([[Cross Validation|link]])
# Evaluation metrics
## Classification
Evaluation metrics for classification models include:
- **Accuracy** - In how many percent of cases the model is correct ([[Accuracy of a ML model|link]])
- **Precision** - An accuracy but only for predictions for a specific class ([[Precision of a ML model|link]])
- **Recall** - Model's effectiveness in detecting samples of a specific class ([[Recall of a ML model|link]])
- **F1 score** - Combination of a precision and recall (trying to balance both) ([[F1 score of a ML model|link]])
- **ROC-AUC** - Helps with choosing a classification threshold ([[ROC-AUC for evaluating ML models|link]])
- **Confusion Matrix** - Shows number of cases when model predicted class A while the true class was B for different classes ([[Confusion matrix|link]])
## Regression
Evaluation metrics for regression models include:
- **RMSE (Root Mean Squared Error**) - An average error ([[RMSE (Root Mean Squared Error) of a ML model|link]])
- **R^2** - How well a model explains a variance, how much better it is from a model that always predicts a mean ([[R squared for evaluating a ML model|link]])
