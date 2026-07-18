Tags: [[_Software_Engineering]]
#SoftwareEngineering 

# Introduction
A filesystem must handle crashes. Example problem:
1. Update file metadata.
2. Update file contents.
3. Power failure happens.

The filesystem may become inconsistent.

Journaling solves this by recording planned changes first:
```
Journal:
"I will update file X"

Apply change

Remove journal entry
```

After a crash, the OS can recover and make the filesystem consistent for example by:
- Completing an unfinished operation on a file
- Undoing partial changes that were done before the failure