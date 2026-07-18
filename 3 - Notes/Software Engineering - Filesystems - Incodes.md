Tags: [[_Software_Engineering]]
#SoftwareEngineering 

# Introduction
In many filesystems (e.g., ext4), the file name is separate from the file metadata.

An inode stores information about a file:
```
inode:
 - owner
 - permissions
 - file size
 - timestamps
 - pointers to data blocks
```

Directory stores filename → inode mapping:
```
data.txt → inode 1234
```

Inode stores file metadata + where the data is stored on a disk:
```
inode 1234 → disk blocks 500, 501, 502
```