Tags: [[__Software_Engineering]]
#SoftwareEngineering  

# Introduction
A rolling deployment means updating an application gradually, replacing old instances/pods with new ones gradually instead of replacing everything at once.

For example, suppose you have 3 Kubernetes replicas:
```
Before:
Pod A → v1
Pod B → v1
Pod C → v1
```

Deploy v2:
```
Step 1:
Pod A → v2
Pod B → v1
Pod C → v1

Step 2:
Pod A → v2
Pod B → v2
Pod C → v1

Step 3:
Pod A → v2
Pod B → v2
Pod C → v2
```

During the deployment, the application can **continue serving requests** through the remaining healthy pods.

Kubernetes commonly does this with a `Deployment` using the `RollingUpdate` strategy.

The main benefit is **reduced downtime and lower deployment risk**. If the new pods fail their readiness checks, Kubernetes can stop progressing the rollout rather than immediately replacing everything.

A related concept is **rollback**: if v2 is problematic, you can return to v1.