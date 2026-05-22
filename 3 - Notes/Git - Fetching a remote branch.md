Tags: [[_Git]]
#Git 

# Introduction
If there is a remote branch which we don't have locally, then in order to create a local branch tracking the remote one we need to use:
```shell
git fetch --all
# List remote branches
git branch -r
# create a local branch tracking the remote one
git checkout -b feature-branch origin/feature-branch
````