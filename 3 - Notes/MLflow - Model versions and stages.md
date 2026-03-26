Tags: [[__Machine_Learning_Engineering]] [[_MLflow]]
#MLEngineering #MLflow 

# Versions
When we register a model ([[MLflow - Register a model|link]]), it gets assigned a version (either automatically or we can specify version number). 

Model name together with a version number is a unique identifier of a model (for each model name versions are unique).

Once we assign a version when registering a model, it can't be changed.
# Stages
We can assign stage name to a model (if we don't do this, then it has a `None` stage). We can change stage names whenever we want and they don't need to be unique.