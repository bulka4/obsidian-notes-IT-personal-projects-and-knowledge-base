Tags: [[_Python]] [[__Programming_languages]]
#Python #ProgrammingLanguages 

# Install packages
```bash
RUN apt-get update && \
    apt-get install -y software-properties-common && \
    add-apt-repository ppa:deadsnakes/ppa && \
    apt-get update && \
    apt-get install -y \
        python3.11 \
        python3.11-dev \
        python3.11-venv \
        python3.11-distutils \
        python3-pip \
        curl && \
    rm -rf /var/lib/apt/lists/*
```
where:
   - software-properties-common - Installs add-apt-repository, allow to add external repositories (PPAs)
   - add-apt-repository ppa:deadsnakes/ppa - Add new repo which is a package source (we can install from it newer Python versions)
   - python3.11-dev - Development headers needed to compile Python packages with C extensions. Required for some libraries like NumPy
   - python3.11-venv - venv package for creating virtual environments
   - python3.11-distutils - Utilities used by Python packaging, used during installing libraries with pip
   - python3-pip - Install pip for installing libraries
   - curl - For downloading files from URLs
   - rm -rf /var/lib/apt/lists/* - Remove apt metadata
# Make Python default
Use `update-alternatives` ([[Linux & Bash - update-alternatives|link]]):
```bash
update-alternatives --install /usr/bin/python3 python3 /usr/bin/python3.11 1
```
to make this version of Python the default one (in case when we have multiple Python versions). This will cause that when users will use `/usr/bin/python3` path, it will run the `/usr/bin/python3.11` executable.