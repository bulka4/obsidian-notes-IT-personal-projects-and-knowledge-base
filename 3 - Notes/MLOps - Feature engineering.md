Tags: [[__MLOps]]
#MLOps 

# Introduction
Feature engineering is about creating pipelines which create datasets with features which models use for making predictions.
# Reproducibility
To make feature pipelines reproducible, we use both code and data versioning. This way we can reproduce data used for training models.
# Feature store
We can use a feature store for:
- Documenting features, making it easier to reuse them
- Reading features from an in-memory database for a quick access during a real-time inference
- joining tables with events and features which are defined for a specific time

More info here - [[MLOps - Feature store]].