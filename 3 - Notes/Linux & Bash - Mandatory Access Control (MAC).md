Tags: [[__Infrastructure_Engineering]] [[_Linux & Bash]] [[_Software_Engineering]]
#InfrastructureEngineering #LinuxBash #SoftwareEngineering 

# Introduction
Mandatory Access Control (MAC) is an access control model where security policies are enforced by the operating system and cannot be changed by ordinary users or applications.

The OS decides:
> "Even if you own the file, are you allowed to access it in this context?"

This is different from traditional Linux permissions (Discretionary Access Control, DAC), where the owner of a file can decide who gets access.
# Example
Suppose `nginx` runs as user `nginx`, and this user has read permission to `/home/user/secret.txt`.
- DAC only: `nginx` can read the file.
- MAC (SELinux/AppArmor): the OS may still deny access because the policy says a web server process must not read users' home directories.
# Frameworks
Frameworks that provide MAC:
1. [[Linux & Bash - SELinux]]
2. [[Linux & Bash - AppArmor]]