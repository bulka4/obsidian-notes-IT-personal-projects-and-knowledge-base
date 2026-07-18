Tags: [[__Infrastructure_Engineering]] [[_Linux & Bash]] [[_Software_Engineering]]
#InfrastructureEngineering #LinuxBash #SoftwareEngineering 

# Introduction
**AppArmor** is a Linux security framework that provides **Mandatory Access Control (MAC)** by restricting what programs are allowed to do.

It works by assigning **security profiles** to applications.

Example:
```
/usr/bin/nginx
        |
        ↓
AppArmor profile:
- allow reading /var/www/**
- allow network access on ports 80/443
- deny access to /home/**
- deny modifying system files
```

Even if `nginx` is compromised, the attacker is limited by the AppArmor profile.
# How it works
1. A program starts:
```
nginx process
```

2. The kernel checks its AppArmor profile:
```
"Is nginx allowed to read this file?"
```

3. The kernel allows or denies the operation.
# Main concepts
## Profiles
- Rules describing what an application can access.
- Stored usually in:
```
/etc/apparmor.d/
```

Example:
```
/usr/sbin/nginx {
    /var/www/** r,
    /etc/nginx/** r,
    deny /home/** rw,
}
```
## Modes
- **Enforce**
    - Blocks violations.
- **Complain**
    - Allows actions but logs violations (useful for creating profiles).
# Useful commands
Check status:
```
aa-status
```

Load/reload a profile:
```
sudo apparmor_parser -r /etc/apparmor.d/profile
```

View logs:
```
journalctl | grep apparmor
```