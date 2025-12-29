Tags: [[__Machine_Learning_Engineering]]

# Introduction
Ray Serve checkpoints maintains a persistent snapshot of deployment state so that:
- The system can recover from failures.
- We can restart the cluster and your deployments come back automatically.
- The operator or serve.status() can show the current deployment state.

Specifically, Ray Serve checkpoints:
- The deployment graph (which deployments exist, their replicas, routes).
- The constructor arguments we pass via .bind() or .deploy().
- The attributes created in __init__ of your deployment object.
- Optional deployment-level configuration (replica resources, autoscaling settings).

Anything created after __init__, such as in a separate method called later, is not checkpointed.

Checkpoints are saved in GCS.

We should avoid checkpointing big objects as there is a disk space limit. We can’t checkpoint more than ~500 MB.

So for example we should not create big attributes in the __init__ method (like a ML model).

Also we should not use in the deployment class any big variables defined outside of this class like here we create a big variable called ‘answer_model’:
![[2 - Images/Ray/Screenshot 5.png]]

That’s because variables created outside of the class needs to be read when running the deployment class using the .run() method.

#MLEngineering 