Tags: [[_Software_Engineering]]
#SoftwareEngineering 

# Introduction
A filesystem is the way an operating system organizes, stores, and retrieves data on storage devices (SSD, HDD, etc.).

It provides a logical view of storage:
```
Application
    |
    | open("data.txt")
    ↓
Filesystem
    |
    ↓
Disk blocks
    |
    ↓
SSD/HDD
```

Without a filesystem, a disk would just be a huge sequence of bytes with no concept of files or directories.
# Related topics
- [[Software Engineering - Filesystems - Files and directories]]
- [[Software Engineering - Filesystems - Incodes]]
- [[Software Engineering - Filesystems - Blocks]]
- [[Software Engineering - Filesystems - File descriptors]]
- [[Software Engineering - Filesystems - Journaling]]
- [[Software Engineering - Filesystems - Caching]]
- [[Software Engineering - Filesystems - Filesystem types]]