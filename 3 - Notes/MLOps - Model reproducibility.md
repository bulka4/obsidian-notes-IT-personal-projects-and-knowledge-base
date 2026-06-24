Tags: [[__MLOps]]
#MLOps 

# Introduction
Model reproducibility is about being able to reproduce the same models later on in the future. 

This is done through:
- Creating automated training pipelines (preparing data, training a model, testing it and saving)
- Versioning data and code
# Why it is needed
We need to be able to see how model was created and recreate it for:
- Recover lost model
- Debugging - Determine why model performance dropped after updating the model (compare how models were created)
- Experiment tracking - When comparing experiments, you need confidence that differences in performance come from intentional changes, not accidental variations.
- Model updating - When we want to prepare a new version of a model, it is useful to see how the current model was created. We can use it as a starting point for preparing a new model.
# Data reproducibility
To be able to reproduce a model, we need to be able to reproduce the dataset which was used for training it as described here - [[MLOps - Data reproducibility]]