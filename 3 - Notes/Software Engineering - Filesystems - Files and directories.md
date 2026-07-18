Tags: [[_Software_Engineering]]
#SoftwareEngineering 

# Introduction
A filesystem organizes data into files and directories.

A file has:
- name
- size
- permissions
- timestamps
- location on disk

A directory is also a file but it can contain:
- file names and information about where their data is located:
  ```
	data.txt  → disk blocks 500, 501, 502
	photo.jpg → disk blocks 700, 701
	notes.md  → disk blocks 900
  ```
  - file names and their incodes ([[Software Engineering - Filesystems - Incodes|link]]):
    ```
	data.txt → inode 1234
    ```