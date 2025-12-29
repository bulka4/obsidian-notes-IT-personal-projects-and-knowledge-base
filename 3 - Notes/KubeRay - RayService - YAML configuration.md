Tags: [[__Machine_Learning_Engineering]]

# Introduction
If we have for example a Ray Serve app like this:
![[2 - Images/Ray - Running on Kubernetes/Screenshot 1.png]]

And it is saved as /app/ray_serve_app.zip, then a YAML manifest for RayService will look like this (below are 3 screenshots of the same YAML file):
![[2 - Images/Ray - Running on Kubernetes/Screenshot 2.png]]

![[2 - Images/Ray - Running on Kubernetes/Screenshot 3.png]]
![[2 - Images/Ray - Running on Kubernetes/Screenshot 4.png]]

Here we specify number of replicas of Worker Pods, not Actors. Number of Actors replicas is specified in the Python script with defined Ray Serve app.

I think that our app needs to be save as a .zip file.

#MLEngineering 