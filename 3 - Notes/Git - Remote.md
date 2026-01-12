Tags: [[_Git]]
#Git 

# Introduction
A Remote represents a remote repository (on the internet) to which our local folder is linked to.

It points to a URL of the remote repository.

We can list remotes and corresponding URLs using this command:
```
Git remote -v
```
# Origin remote
A remote called ‘origin’ can be created in a different ways:
- **When cloning a repo** – When we clone a repository using git clone, then URL of the repo we are cloning is automatically assigned as the origin remote.
- **Manually** – We can manually assign URL to the origin using this command: ‘git remote add origin [https://github.com/your/project.git](https://github.com/your/project.git)’