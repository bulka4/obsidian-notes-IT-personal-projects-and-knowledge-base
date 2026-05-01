Tags: [[__Machine_Learning_Engineering]] [[_MLflow]]
#MLEngineering #MLflow 

# Introduction
MLflow allows for experiment tracking, i.e. to save information about models we create and additional artifacts (files), such as:
- Parameters - Hyperparameters used for training like learning rate, batch size, etc.
- Evaluation metrics - Accuracy, loss, AUC, any numeric measure
- Artifacts - Model files, plots, datasets, any output file
- Source info - Git commit hashes, code version, who ran it, when

We can create a script which trains or evaluates a model and saves metadata, for example:
```python
x_train = ...
y_train = ...
model = ...
model.fit(x_train, y_train)

y_pred = model.predict(x_test)
mse = mean_squared_error(y_test, y_pred)
r2 = r2_score(y_test, y_pred)

with mlflow.start_run() as run:
    # Log parameters used
    mlflow.log_param("learning_rate", 0.01)
    # Log metrics
    mlflow.log_metric("mse", mse)
    mlflow.log_metric("r2", r2)
```