Tags: [[_Git]]
#Git 

# Introduction
The `git fetch origin` command:
- Connects to the remote repository called 'origin'
- Downloads ne commits, branches and tags
- Updates remote-tracking branches such as origin/main
- But it doesn't change local files

After fetching we can change our local files so they match those from the remote repository. For example we can use `git reset --hard origin/<branch-name>` to remove local changes and apply all the changes from the remote, from a given branch.

Then all of our local files will be exactly the same as those in the remote repository.