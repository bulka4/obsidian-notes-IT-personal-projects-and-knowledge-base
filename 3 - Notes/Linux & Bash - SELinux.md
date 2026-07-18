Tags: [[__Infrastructure_Engineering]] [[_Linux & Bash]] [[_Software_Engineering]]
#InfrastructureEngineering #LinuxBash #SoftwareEngineering 

# Introduction
**SELinux (Security-Enhanced Linux)** is a Linux security framework that provides **Mandatory Access Control (MAC)** by enforcing security policies based on **labels attached to processes and resources**.

Its goal is:
> Even if a user or process has normal Linux permissions, SELinux can still deny access if the security policy does not allow it.
# How it works
Everything gets a **security context (label)**:

Example:
```
Process:
nginx → httpd_t

Files:
website files → httpd_sys_content_t
SSH keys      → ssh_home_t
```

SELinux rules define which labels can interact:
```
httpd_t  → can read → httpd_sys_content_t
httpd_t  → cannot read → ssh_home_t
```

So a compromised web server cannot automatically access sensitive files.
# Example
Without SELinux:
```
nginx process
    |
    └── user permissions allow reading:
        /home/user/.ssh/id_rsa
```

With SELinux:
```
nginx process (httpd_t)
    |
    └── denied:
        /home/user/.ssh/id_rsa (ssh_home_t)
```

The kernel blocks it.
# Modes
SELinux has three modes:
- **Enforcing**
    - Block forbidden actions and log them.
- **Permissive**
    - Allow actions but log violations (used for debugging).
- **Disabled**
    - Completely off.

Check status:
```
sestatus
```
# Important concepts
## Labels (contexts)
View labels:
```
ls -Z
```

Example:
```
-rw-r--r-- user user system_u:object_r:httpd_sys_content_t file.html
```
## Policies
Define allowed interactions:
```
Process type → allowed → Resource type
```