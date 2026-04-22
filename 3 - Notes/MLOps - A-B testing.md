Tags: [[__MLOps]]
#MLOps 

# Introduction
A/B testing is a method similar to a canary deployment ([[MLOps - Canary & shadow deployment|link]]), i.e. a method to compare two models by distributing a traffic between both models (forwarding data inputs to both to make predictions) and comparing how they perform.

The only difference is that we don't forward to one model only a small part of a traffic (like 10%) but we distribute a traffic equally between the two models (50% each).