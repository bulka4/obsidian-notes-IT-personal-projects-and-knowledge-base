Tags: [[__MLOps]]
#MLOps 

# Introduction
Both canary and shadow deployment are techniques of deploying a ML model. Both are used to test how a new model performs before fully replacing an old model with it.
# Canary deployment
In a canary deployment, we use a new model on a small part of a traffic (it makes predictions for a small part of data inputs).
# Shadow deployment
In a shadow deployment, we run a new model in parallel with an old one (both makes predictions for the same data inputs) but predictions of the new model are not used, we only observe how good are those predictions.