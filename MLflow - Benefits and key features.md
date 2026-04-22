Tags: [[__Machine_Learning_Engineering]] [[_MLflow]]
#MLEngineering #MLflow 

# Saving models with metadata
We can run a script which trains or evaluates a model and logs metadata about the process, such as:
- hyperparameters used
- data used (SQL query)
- code version used
- evaluation metrics

Also, it can save artifacts such as:
- model itself
- graphs visualizing model performance during evaluation
- any other file

All that information can be linked, so we will know that a specific logged metadata corresponds to a specific saved model.

To saved models we can assign versions, stages and aliases ([[MLflow - Registry|link]]) what helps with managing them.

Thanks to those artifacts and logs we get following benefits:
## Simplified deployment
All the models are saved in a single place with assigned stages, tags and additional metadata, for example about how they performed during evaluation.

For example, we can create a deployment process such that we:
- Pick a model with the best metrics
- Save it in a location from where it will be used in a production pipeline
## Reproducibility
Understand exactly how each model was produced thanks to the saved metadata and recreate it.
## Comparing models
Compare models' performance during evaluation.
# Compatibility with other frameworks
MLflow works with many other frameworks like TensorFlow, PyTorch, Scikit-learn, Spark ML, etc.
# Collaboration & governance
Teams can share experiments, compare models, and manage lifecycle stages (Staging → Production) in a controlled way.
# Code packaging
We can create MLflow projects ([[MLflow - Projects|link]]) which contains:
- Scripts to run
	- For example for training or evaluating a model
	- They can be parametrized, so we can provide input parameters like what data or hyperparameters to use
- Instruction about how to prepare an environment for running project's scripts
	- For example, we can provide a Dockerfile and MLflow will run a container and run a script in it [[MLflow - Docker execution mode|link]])