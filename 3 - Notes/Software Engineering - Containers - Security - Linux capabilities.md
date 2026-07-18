Tags: [[_Software_Engineering]]
#SoftwareEngineering 

# Introduction
Linux splits root privileges into smaller permissions called **capabilities**.

Instead of giving full root:
```
root
 |
 +-- CAP_NET_ADMIN
 +-- CAP_SYS_TIME
 +-- CAP_SYS_ADMIN
 ...
```

A container can receive only what it needs.

Example:
```
--cap-drop ALL
--cap-add NET_BIND_SERVICE
```

Meaning:
- remove all privileges
- allow only binding to low network ports