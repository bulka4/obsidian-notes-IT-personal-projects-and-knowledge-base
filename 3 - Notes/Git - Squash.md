Tags: [[_Git]] [[_Software_Engineering]]
#Git #SoftwareEngineering 

# Introduction
Git squash means combining multiple commits into one commit. It is usually done with interactive rebase.
# Example
You have a feature branch:

```
main:     A---B---C
                   \
feature:            D---E---F---G
```

Maybe your commits are messy:
```
D: add login button
E: fix typo
F: fix another bug
G: refactor login code
```

Before merging, we can squash them. We start with performing an interactive rebase which opens an editor:
```
git rebase -i main
```

and in that editor, we can mark commits as `squash`:
```
pick D add login button
squash E fix typo
squash F fix another bug
squash G refactor login code
```

Git combines them into one new commit:
```
main:     A---B---C
                   \
feature:            H
```

where `H` contains all changes from `D+E+F+G`.
# Why squash?
- Creates a cleaner history.
- Avoids having many small "fix typo" commits in `main`.
- Makes each merged feature a single meaningful commit.