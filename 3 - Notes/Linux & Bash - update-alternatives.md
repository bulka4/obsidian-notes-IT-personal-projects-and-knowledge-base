Tags: [[__Infrastructure_Engineering]] [[_Linux & Bash]]
#InfrastructureEngineering #LinuxBash 

# Introduction
The `update-alternatives` tool allows to have multiple versions of the same tool installed and choose which one is the default.

Syntax:
```bash
update-alternatives --install <symlink> <group-name> <path-to-version> <priority>
```
Example:
```bash
update-alternatives --install /usr/bin/python3 python3 /usr/bin/python3.11 1
```
where:
- `<symlink>` → the path that users will call (here: `/usr/bin/python3`)
- `<group-name>` → the “group name” for alternatives (here: `python3`)
- `<path-to-version>` → the actual binary to use (here: `/usr/bin/python3.11`)
- `<priority>` → an integer; higher priority becomes the default if auto mode is enabled (here: `1`)

So when users run `/usr/bin/python3` (the `symlink`), the `/usr/bin/python3.11` binary (the `path-to-version` ) will be executed.

The group name is only used within the `update-alternatives` to help managing multiple versions of the same tool, it is not name used by users to run the binary (it doesn't define what will happen when users run `group-name` command).