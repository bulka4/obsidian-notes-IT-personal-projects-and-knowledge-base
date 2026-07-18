Tags: [[_Software_Engineering]]
#SoftwareEngineering 

# Introduction
When a program opens a file:
```
f = open("data.txt")
```
the OS returns a file descriptor (which is a number) which can be then used to perform operations on that file, for example to read data from it or to write to it.

The program does not directly work with the disk but it makes system calls ([[Software Engineering - Operating systems - System calls|link]]) to get a file descriptor or to use that descriptor to perform different actions on the file.