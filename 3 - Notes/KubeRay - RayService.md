Tags: [[__Machine_Learning_Engineering]]

# Introduction
RayService can be used to create a Ray cluster (Head and Worker Pods) and run on it Ray Serve apps.

It deploys a proxy (HTTP gateway, Starlette ASGI) on the Head Pod by default.

This proxy receives clients requests and forwards them to a proper Actor replica.

We can also create multiple proxy replicas and then some of them will run on Worker Pods as well.

More information about it, can be found in the below documents:
- YAML configuration - [[KubeRay - RayService - YAML configuration|link]]
- Installing RayService - flow of events - [[KubeRay - Installing RayService - flow of events|link]]

#MLEngineering 