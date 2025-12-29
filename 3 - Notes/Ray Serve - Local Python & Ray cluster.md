Tags: [[__Machine_Learning_Engineering]]

# Introduction
When you define a deployment, you need to deploy it into a running Ray cluster, for example:
![[2 - Images/Ray/Screenshot 2.png]]

In this case we need to have a Ray cluster running and run this script on one of the cluster’s nodes.

We can also use the serve.run() function which enables creating multiple deployments:
![[2 - Images/Ray/Screenshot 3.png]]

#MLEngineering 