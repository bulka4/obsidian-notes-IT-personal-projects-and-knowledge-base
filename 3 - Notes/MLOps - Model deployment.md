Tags: [[__MLOps]]
#MLOps 

# Introduction
By deploying a model we mean preparing it to be used in production, that is:
- Package and version the model
- Make it reproducible

So we save a model in a place from where it can be picked up by other users / processes.

Once model is deployed, it can be used in production for either:
- Creating a Rest API that serves model inference (online scoring, [[MLOps - Model serving|link]])
- Or creating batch inference processes ([[MLOps - Batch inference|link]]) (offline inference)