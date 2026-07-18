Tags: [[_Git]] [[_Software_Engineering]]
#Git #SoftwareEngineering 

# Introduction
**`git cherry-pick`** copies one or more specific commits from one branch and applies them onto another branch.
# Example
You have:
```
main:      A---B---C
                 \
feature:          D---E---F
```

You want only commit `E` from `feature` on `main`.

You run:
```
git checkout main
git cherry-pick E
```

Result:
```
main:      A---B---C---E'
                 \
feature:          D---E---F
```

`E'` is a **new commit** with the same changes as `E`, but a different commit ID.
# Why use cherry-pick?
Common cases:
- **Bring a bug fix from another branch**
  Example:
    - A bug is fixed on a development branch.
    - You want the fix immediately on a production branch.
    - Cherry-pick only that fix.
- **Copy a useful commit without merging the whole branch**