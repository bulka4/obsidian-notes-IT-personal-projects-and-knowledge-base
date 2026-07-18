Tags: [[_Git]] [[_Software_Engineering]]
#Git #SoftwareEngineering 

# Introduction
**Git rebase** is a way to move or replay commits from one branch onto another branch.
# Example
```
main:    A---B---C
              \
feature:       D---E
```

If `main` gets new commits:
```
main:    A---B---C---F---G
              \
feature:       D---E
```

You can run:
```
git checkout feature
git rebase main
```

Git will take your feature commits (`D`, `E`) and replay them on top of the latest `main`:
```
main:    A---B---C---F---G
                         \
feature:                  D'---E'
```

`D'` and `E'` are new commits (same changes, different commit IDs).
# Merge vs rebase
**Merge:**
```
A---B---C---F---G
     \       /
      D---E
```

Creates a merge commit.

**Rebase:**
```
main:    A---B---C---F---G
                         \
feature:                  D'---E'
```

No merge commit, we still have a separate branch.

If we now merge after a rebase, we get one branch with a straight history:
```
A---B---C---F---G---D'---E'
```
