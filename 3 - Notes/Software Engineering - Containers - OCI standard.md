Tags: [[_Software_Engineering]]
#SoftwareEngineering 

# Introduction
**OCI (Open Container Initiative)** is an open standard that defines how containers should be packaged and run.

The goal is:
> Make container images and runtimes compatible across different tools.

Before OCI, Docker had its own formats. OCI created common specifications so tools like Docker, containerd, Kubernetes, and Podman can work together.
# Specifications
## 1. Image Specification
Defines how a container image is structured.

Example:
```
Container image
 |
 +-- Manifest
 |
 +-- Config
 |
 +-- Layers
```

Defines:
- image format
- metadata
- layer structure
- content addressing
## 2. Runtime Specification
Defines how a container should be executed.

It specifies things like:
- how to create a container
- how to start/stop it
- filesystem setup
- namespaces
- cgroups

Example:
```
containerd
    |
    ↓
runc (OCI runtime)
    |
    ↓
Linux kernel
```
## 3. Distribution Specification
Defines how container images are transferred between:
- registries
- clients
- runtimes

Example:
```
Developer
   |
docker push
   |
Container Registry
   |
docker pull
   |
Server
```