Tags: [[__MLOps]]
#MLOps 

# Introduction
Model versioning is about keeping models saved and assigning to them different versions / tags / stages.

For example, w can:
- Have multiple versions of the same model saved
- Only one model has assigned stage 'Production' and this one is used in production pipelines for making predictions
- When model starts performing poorly and we create a new, better model, we can move this new model to the 'Production' stage, replacing the old one, and this way it will be now used in production pipelines.