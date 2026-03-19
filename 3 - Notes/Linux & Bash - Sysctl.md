Tags: [[__Infrastructure_Engineering]] [[_Linux & Bash]]
#InfrastructureEngineering #LinuxBash 

# Introduction
It is used to view and modify kernel parameters without rebooting the system.

Those parameters control how Linux kernel behaves, including things like:
- Networking settings
- Memory limits
- Process handling
- Security controls

Those parameters are stored in the /proc/sys/ directory.

If we change some parameters using the sysctl command, then those changes are not persistent across reboots.

If we want them to be consistent we need to create a .conf file in the /etc/sysctl.d/ folder and save those changes there.

For example this command:
- `sysctl -w net.ipv4.ip_forward=1`

changes the `net.ipv4.ip_forward` parameter which is stored in the /proc/sys/net/ipv4/ip_forward file.

If we want to have this parameter set up like this across reboots then we need to create a file like this:
- `echo “net.ipv4.ip_forward=1” > /etc/sysctl.d/filename.conf`