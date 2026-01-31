Tags: [[_Git]] [[_Kubernetes]]
#Git #Kubernetes 

# Introduction
When we create a Pod on Kubernetes ([[Kubernetes - Pod|link]]), we can run git-sync as a sidecar container in that Pod. 

The Pod defines a shared volume, which is mounted by both git-sync and the main application container.  

git-sync periodically pulls code from a Git repository and writes it into that volume, making the files available to the other container in the Pod.

To run git-sync in a sidecar container, we use the git-sync Docker image.