Tags: [[_kind]] [[__Cloud]], [[__DevOps]], [[__Distributed_computing]], [[__Infrastructure_Engineering]]
#kind #Cloud #DevOps #DistributedComputing #DataEngineering 

# Introduction
To make available code to execute in pods we run, we have four options:
- Include code in the image
- Run an init container which pull code from a repo
- Use git-sync running in a separate pod / sidecar container
- Use a PV with a hostPath
- Use a PV with Azure File share
# Init container pulling code
If we want to run code in a pod which will be finished after a specific amount of time, it is good to use an init container which pulls code from a repo using git.

Pros:
- Simple, we don't need to create extra pods and PVs

Cons:
- Pods start is slightly delayed as we need to wait for code to be pulled
# Git-sync
We can use git-sync which runs in a separate pod or sidecar container and which:
- Pulls code from a repo systematically, once per specified period of time
- Saves code in a PV
- Other pods / containers can take that code using a PV connected to the same storage

When deployed on kind, it saves data in the `git_code` folder.

More details about how git-sync works can be found here - [[Git-sync - Kubernetes deployment]].

It is good when we run in a pod a long-running service, which is supposed to run all the time, not finish in a specific period. The benefit is that we have the latest code available all the time.

If we one git-sync pod which saves code in a PV which is then used in many other pods, then it has the following pros and cons:
- Pros:
	- When we start a new pod, it doesn't wait to code to be pulled, it takes already pulled code from a PV
	- There is only one pod pulling the code and code is stored only in one place (Azure File share)
- Cons
	- All the pods uses the same code (we might want to get code from a different repo, commit or branch for different pods)
## Preparing a PV
In order to make the pulled code available for other pods, we need to create a PV in the pod's namespace and link it to the same storage where git-sync saved the code (we can use the same PV manifest as in the git-sync Helm chart).
# PV with a hostPath
When using kind, we can create a PV with a hostPath to make the code from the host available in pods.
# PV with Azure File share
If we want to run a pod in AKS, then another option for making code available in that pod except for pulling that code from git, is to use a PV which uses Azure File share as a storage and upload code there.