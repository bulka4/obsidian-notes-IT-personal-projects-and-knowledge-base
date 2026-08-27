Tags: [[_Python]] [[__Programming_languages]]
#Python #ProgrammingLanguages 

# Absolute imports
When using absolute imports, Python looks for a module in the module search path `sys.path` ([[Python - Module search path sys.path|link]]).

For example, for a file structure like this:
```
project/
|-- main.py
|-- module/
	|-- functions.py
	|-- variables.py
```

we can make an absolute import like this in the `main.py` file:
```python
# main.py
from module.functions import function 
```

or like this in the `functions.py` file:
```python
# functions.py
from module.variables import function 
```

and Python will look for the `module/functions` and `module.variables` paths in the `sys.path` and it will find them if we run the `main.py` script.
# Relative imports
Relative imports are done in packages. To make a relative import, we need to include dots at the beginning of the package name from which we import.

If we have for example a file structure like this:
```
project/
|-- main.py
|-- module/
	|-- functions.py
	|-- variables.py
```

then `module` is interpreted as a package and in this package we make a relative import, for example in the `functions.py` file like this:
```python
# functions.py
from .variables import x
```

The dot `.` at the beginning of the module's name `.variables` means to use the current package, which in this case is `module`.

Double dots `..` would mean to use the parent package of the current package, i.e. a package containing the `module` package, i.e. the entire `project` package.
# Absolute import equivalent to the relative one
For a file structure like this:
```
project/
|-- main.py
|-- module/
	|-- functions.py
	|-- variables.py
```

we can make a relative import in the `functions.py` file:
```python
# functions.py
from .variables import x
```

Or equivalently, we can use an absolute import like this:
```python
# functions.py
from module.variables import x
```

This will work when running `python main.py` because `module/variables` is in the `sys.path` when running `python main.py`.
# Common errors
For a file structure like this:
```
project/
|-- main.py
|-- module/
	|-- functions.py
	|-- variables.py
```

Such an import in the `functions.py` file will not work when running `python main.py`:
```python
# functions.py
from variables import x
```

 because `variables` is not in the `sys.path` when running `python main.py` and we didn't include dots at the beginning of the module name `variables` so this is not treated as a relative import.

