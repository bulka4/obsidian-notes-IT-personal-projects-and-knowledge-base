Tags: [[_Git]]
#Git 

# Introduction
A tracking branch is a local branch that tracks / corresponds to a branch on a remote.

Here is described how to set up tracking:
- **Automaticly on clone** – When we clone a repo using git clone, then the local main branch is automatically assigned as a tracking branch of the main branch from the remote
- **Manually create a new branch** – When using ‘git checkout -b local_branch remote_branch’, we are creating a local branch called local_branch and we set it up as a tracking branch of the remote branch called remote_branch.
- **Manually when pushing** – When we push code using ‘git push -u origin remote_branch’, then the local branch from which we are pushing code is getting assigned as a tracking branch of the remote branch called remote_branch. A remote branch will be created if it doesn’t exist.

We can check which local branches correspond to which remote ones using this command:
- Git branch -vv

This shows output like this:
![[2 - Images/Git/Screenshot 1.png]]

On the left hand side we have local branch names, and on the right hand, in square brackets we have a corresponding remote branch name and name of a remote to which that branch belongs.

If there are not brackets, that means that the local branch doesn’t track any remote one.

So here local main correspond to the main branch from the origin remote, and hotfix/ui is not tracking any remote branch.