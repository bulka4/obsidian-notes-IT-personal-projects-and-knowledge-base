Tags: [[_Git]] [[_Software_Engineering]]
#Git #SoftwareEngineering 

# Introduction
**`git bisect`** is a tool for finding which commit introduced a bug using **binary search**.

Instead of checking every commit manually, Git narrows the search space.
# Example
You have:
```
A---B---C---D---E---F---G---H
```

You know:
- `A` works
- `H` is broken

You run:
```
git bisect start
git bisect bad H
git bisect good A
```

This way we tell git that the bug is between the commit H and A and Git checks out a commit in the middle, that is:
```
A---B---C---D---E---F---G---H
            ^
          test here
```

You test it:
- If it is broken:
```
git bisect bad
```

- If it works:
```
git bisect good
```

Git keeps jumping halfway until it finds the first bad commit. So for example if we say `git biscet good`, git will check the commit `F` (in the middle on the right).

At the end:
```
A---B---C---D---E---F---G---H
                ^
          bug introduced here
```

Git tells you:
```
commit E
Author: ...
Message: Add new caching logic
```

Then you finish:
```
git bisect reset
```