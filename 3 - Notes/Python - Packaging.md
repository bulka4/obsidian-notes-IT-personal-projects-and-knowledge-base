Tags: [[_Python]] [[__Programming_languages]] [[_Software_Engineering]]
#Python #ProgrammingLanguages #SoftwareEngineering 

# Introduction
Packaging in Python is the process of organizing, distributing, and installing Python code as reusable packages.

A package usually contains:
- Python modules (`.py` files)
- Metadata (name, version, dependencies)
- Configuration files describing how to build/install it
# How to create a package
To create a package, we just need to put the `__init__.py` file in a folder (this file can be empty).

For example like this:
```
|-- my_package/
	|-- __init__.py
	|-- module.py
```
# How to run a package
To run a package, we need to run the following command from the directory containing the package:
```bash
python -m my_package.module
```
# Example package
```
my_package/
│
├── my_package/
│   ├── __init__.py
│   ├── utils.py
│   └── models.py
│
├── pyproject.toml
└── README.md
```

`pyproject.toml` defines how the package is built:
```
[project]
name = "my-package"
version = "1.0.0"
dependencies = [
    "requests"
]
```

Then it can be installed:
```
pip install my-package
```
# Common tools
- **pip** → installs packages
- **PyPI** → public package repository
- **setuptools / Poetry / Hatch / uv** → build and manage packages
- **virtual environments** → isolate dependencies
# Why packaging matters
- Share code between projects
- Publish libraries
- Manage dependencies and versions
- Deploy applications reliably