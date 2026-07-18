Tags: [[_Git]]
#Git 

# Introduction
When we merge another branch with the current one, then we bring code changes from this branch to the current one.

Changes in the current branch are preserved though, we are only adding new changes from another branch.  
# Example
For example, when we have branches and commits like:
```
main: A - B - C - D - E
			\       /
feature:     C' - D'
```

then merge creates a new commit E where git tries to combine:
- All the changes from the feature branch, i.e. changes between commits `D'` and `B`
- All the changes from the main branch, i.e. changes between commits `D` and `B`

So:
- All the changes in the `main` branch are preserved
- And we additionally add changes from the `feature` branch

After merging our new branch still exists and both branches, the new one and the main one, point to the same last commit.

So usually we want to merge our branch with the main one and then push a code.
# Commands
We do this using those commands:
- `git switch main` <- Go to the main branch
- `git merge new_branch` <- Merge our new branch to the main one
- `git push origin main`
# New commit
When we merge a branch, there is a new commit being done for that merge. In that commit, we can see all the changes made by the merge (new changes from the merged branch).
# Squash merge
We can perform a squash merge, that means that all the commits from the merged branch, are squashed into a single, new commit for merge.

In the branch where we merged into, we will not see all the commits from the merged branch, only one new commit.

In the merge request we will be able to see individual commits from the merged branch.