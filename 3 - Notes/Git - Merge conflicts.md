Tags: [[_Git]] [[_Software_Engineering]]
#Git #SoftwareEngineering 

# Introduction
A merge conflict happens when Git cannot automatically decide how to combine changes from two branches.

If both branches edited the same line of code, git can't decide which version is correct.
# Example
For example, when we have branches and commits like:
```
main: A - B - C - D - E
			\       /
feature:     C' - D'
```

then merge tries to combine:
- All the changes from the feature branch, i.e. changes between commits `D'` and `B`
- All the changes from the main branch, i.e. changes between commits `D` and `B`

If changes for both branches edited the same line of code, for example:
- feature branch updated the line 10 into `print('A')`
- main branch updated the line 10 into `print('B')`

then we need to manually change lines which are causing the conflict in one of the branches.
# Resolving conflicts
To fix conflicts, we need to manually change lines which are causing the conflict. Here's how the entire workflow when resolving a conflict looks like:
## Starting point
You have:
```
        C  <- main
       /
A---B
       \
        D  <- feature
```

Meaning:
- `B` is the common ancestor.
- `main` has commit `C`.
- `feature` has commit `D`.

Assume:
- `C` changes `file.txt`:
```
Hello Git
```

- `D` changes the same line:
```
Hello ChatGPT
```
## Step 1: Start the merge
You are on `main`:
```
git checkout main
```

`HEAD` points to:
```
C <- main
```

Then:
```
git merge feature
```

Git tries to create a merge commit:
```
        C
       / \
A---B     M  <- main
       \ /
        D
```

where `M` should contain:
- changes from `C`
- changes from `D`

However, Git cannot decide how to combine them.
## Step 2: Conflict happens
**No commit is created.**

The repository is temporarily in this state:
```
        C  <- main (HEAD)
       /
A---B
       \
        D  <- feature
```

There is no `M` yet.

But your working directory is modified.

The existing file:
```
file.txt
```

is changed to:
```
<<<<<<< HEAD
Hello Git
=======
Hello ChatGPT
>>>>>>> feature
```

This file is **not part of any commit yet**.

It is an uncommitted working tree change.

You can think of it as:
```
Commit C:
file.txt = Hello Git

Commit D:
file.txt = Hello ChatGPT

Working directory:
file.txt = conflict markers
```
## Step 3: Resolve the conflict
You edit the file:
```
Hello Git and ChatGPT
```

Now:
```
Commit C:
Hello Git

Commit D:
Hello ChatGPT

Working directory:
Hello Git and ChatGPT
```

Still, no commit exists.
## Step 4: Stage and commit
You run:
```
git add file.txt
git commit
```

Now Git creates the merge commit:
```
        C-------M  <- main
       /       /
A---B          /
       \      /
        D-----
              ^
           feature
```

Commit `M` contains:
- Parent 1: `C` (main before merge)
- Parent 2: `D` (feature before merge)

The snapshot stored in `M` contains:

```
file.txt = Hello Git and ChatGPT
```