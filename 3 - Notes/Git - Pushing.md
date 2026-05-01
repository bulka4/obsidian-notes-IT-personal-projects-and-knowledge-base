Tags: [[_Git]]
#Git 

# Introduction
We can push our local code to a remote repository using this command:
```shell
git push <remote> <branch>
```
Where:
- `<remote>` - Name of the remote repository where we want to push code. The default one is origin.
- `<branch>` - Name of the local branch from which we are pushing code.

We can skip using the `<branch>` if this branch is already present in the remote. Then, we will push the branch currently used locally.

We can skip using `<remote>`, if we once use:
```shell
git push -u <remote>
```
After that, git will remember to use that specific `<remote>`.