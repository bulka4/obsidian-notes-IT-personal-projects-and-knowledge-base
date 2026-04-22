Tags: [[__Machine_Learning_Engineering]]

# Introduction
MLflow registry is a centralized model store where we manage the lifecycle of your ML models:
- Versioning: Keep track of every model version registered
- Stage transitions: Move models through stages like Staging, Production, Archived
- Annotations & comments: Add notes or tags on model versions
- Deployment integration: Some frameworks can deploy directly from the registry
- Easy model loading: Load a model using its name and version

It brings model governance and collaboration to our ML pipeline.

It is not a separate storage than artifact store ([[MLflow - Tracking server|link]]) but only a logical structure in that store.
# Versions and stages
Each model in a registry gets assigned a version and stage like described here - [[MLflow - Model versions and stages]].
# Aliases
We can assign aliases to models like explained here - [[MLflow - Model aliases]].

#MLEngineering 