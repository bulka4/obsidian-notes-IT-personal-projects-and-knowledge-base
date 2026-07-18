Tags: [[__Infrastructure_Engineering]] [[_Linux & Bash]] [[_Software_Engineering]]
#InfrastructureEngineering #LinuxBash #SoftwareEngineering 

# Introduction
Linux permissions control **who can access files and execute programs**.
# Users and groups
Linux has:
- **User** – an individual account (`marcin`, `postgres`, `nginx`)
- **Group** – a collection of users (`developers`, `docker`)
- **Others** – everyone else

Every file and directory has:
- an **owner user**
- an **owner group**

Example:
```
-rw-r----- 1 marcin developers file.txt
```

Here:
- owner user: `marcin`
- owner group: `developers`
# Permission types
There are three basic permissions:

|Permission|Symbol|Value|Meaning|
|---|---|---|---|
|Read|`r`|4|View file contents|
|Write|`w`|2|Modify file|
|Execute|`x`|1|Run program / enter directory|

Permissions are specified for:
```
Owner | Group | Others
```

Example:
```
-rwxr-x---
```

means:

| Entity | Permissions |
| ------ | ----------- |
| Owner  | `rwx` (7)   |
| Group  | `r-x` (5)   |
| Others | `---` (0)   |
# Directories
For directories:
- `r` → list files inside (`ls`)
- `w` → create/delete files
- `x` → enter the directory (`cd`)

A directory without `x` cannot be entered even if you can list its contents.