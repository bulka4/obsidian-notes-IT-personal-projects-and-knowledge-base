Tags: [[_Python]] [[__Programming_languages]]
#Python #ProgrammingLanguages 

# Introduction
The `sys.path` variable is a module search path. It contains paths where Python looks for modules when importing them.

The `sys.path` always contains the current folder from which we run a Python script. For example, when we have a file structure like this:
```
/project/
|-- main.py
|-- some_class.py
|-- module/
	|-- functions.py
	|-- variables.py
```

and we run the Python script from the `/project` folder:
```shell
# Running in the '/project' folder
python main.py
```

then path to the `/project` folder will be in the `sys.path`.

When importing a module, Python will look whether this module is at one of the paths from the `sys.path`.

For example, we can import `import some_class` or `import module.functions` because `some_class.py` and `module/functions.py` files are at the path to the `/project` folder.
# Adding paths to the `sys.path`
We can also add new paths to the `sys.path`. For example, if we add `module`:
```python
sys.path.append('/project/module')
```

then we can import functions from the `module` folder like this:
```python
import functions
```

We don't need to use `import module.functions` because path to the `module` folder is already in the `sys.path`.