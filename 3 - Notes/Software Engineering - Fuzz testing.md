Tags: [[__Software_Engineering]]
#SoftwareEngineering 

# Introduction
Fuzz testing (fuzzing) is a testing technique where we automatically provide a program with many random, unexpected, extreme or malformed inputs to find bugs, crashes, security vulnerabilities, or unexpected behavior.

The idea:
> "Give the system inputs it was not designed for and see if it breaks."

We don't use invalid inputs but those which we think are less likely. For example, if we have a function where we expect a name as an input:
```python
def get_user(name):
    ...
```
we might provide inputs such as:
```
""
" "
"aaaaaaaaaaaaaaaaaaaa..."   # extremely long
"😀🔥"
"\0"
"'; DROP TABLE users; --"
"\n\n\n"
random binary data
```
