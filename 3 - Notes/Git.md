Tags: [[__DevOps]]

# Branches

## Commits

We can create a branch and each branch can have its own commits.

When we create a new branch, it contains all the commits made so far, but when we make a new commit, it is visible only on this one branch.

When we merge our branch to the main one, then all the commits made on our new branch become visible from the main one.

## Merging

When we merge another branch with the current one, then we bring code changes from this branch to the current one.

Changes in the current branch are preserved though, we are only adding new changes from another branch.  
For example, when we are on the main branch, and we run 'git merge new_branch' command, then all the code changes from the new_branch branch are applied to the main branch (our local files are being changed).

After merging our new branch still exists and both branches, the new one and the main one, point to the same last commit.

So usually we want to merge our branch with the main one and then push a code.

We do this using those commands:

· Git switch main <- Go to the main branch

· Git merge new_branch <- Merge our new branch to the main one

· Git push origin main

## Tracking branch

A tracking branch is a local branch that tracks / corresponds to a branch on a remote.

Here is described how to set up tracking:

· **Automaticly on clone** – When we clone a repo using git clone, then the local main branch is automatically assigned as a tracking branch of the main branch from the remote

· **Manually create a new branch** – When using ‘git checkout -b local_branch remote_branch’, we are creating a local branch called local_branch and we set it up as a tracking branch of the remote branch called remote_branch.

· **Manually when pushing** – When we push code using ‘git push -u origin remote_branch’, then the local branch from which we are pushing code is getting assigned as a tracking branch of the remote branch called remote_branch. A remote branch will be created if it doesn’t exist.

We can check which local branches correspond to which remote ones using this command:

· Git branch -vv

This shows output like this:
![[2 - Images/Git/Screenshot 1.png]]

On the left hand side we have local branch names, and on the right hand, in square brackets we have a corresponding remote branch name and name of a remote to which that branch belongs.

If there are not brackets, that means that the local branch doesn’t track any remote one.

So here local main correspond to the main branch from the origin remote, and hotfix/ui is not tracking any remote branch.

# Pushing

We can push our local code to a remote repository using this command:
```
Git push <remote> <branch>
```
Where:

- \<remote\> - Name of the remote repository where we want to push code. The default one is origin.
- \<branch\> - Name of the local branch from which we are pushing code.

# Remote

A Remote represents a remote repository (on the internet) to which our local folder is linked to.

It points to a URL of the remote repository.

We can list remotes and corresponding URLs using this command:
```
Git remote -v
```
## Origin remote

A remote called ‘origin’ can be created in a different ways:

· **When cloning a repo** – When we clone a repository using git clone, then URL of the repo we are cloning is automatically assigned as the origin remote.

· **Manually** – We can manually assign URL to the origin using this command: ‘git remote add origin [https://github.com/your/project.git](https://github.com/your/project.git)’

# Pulling

Using the ‘git pull’ command we can pull code from a remote to our local folder.

This way we are applying all the changes from the the remote which we don’t have locally. So it modified our local files but changes which we have locally but they are not in a remote, they are preserved.
# Fetching
The `git fetch origin` command:
- Connects to the remote repository called 'origin'
- Downloads ne commits, branches and tags
- Updates remote-tracking branches such as origin/main
- But it doesn't change local files

After fetching we can change our local files so they match those from the remote repository. For example we can use `git reset --hard origin/<branch-name>` to remove local changes and apply all the changes from the remote, from a given branch.

Then all of our local files will be exactly the same as those in the remote repository.