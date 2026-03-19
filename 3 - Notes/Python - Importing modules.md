Tags: [[_Python]] [[__Programming_languages]]
#Python #ProgrammingLanguages 

# Relative module path
When we have for example a file structure like this:
```bash
root/
 ├─ main.py
 └─ common/
      ├─ script_1.py
      └─ script_2.py
```

and in the `main.py` we have:
```python
from common.script_1 import something
```

and in the `script_1.py` we have:
```python
from script_2 import something
```

then running `python main.py` will not work because `script_2.py` is not in the `sys.path` which `main.py` is using.

Instead, we should write in the `script_1.py`:
```python
from .script_2 import something
```

That dot `.` makes sure that when importing `something` from the module `script_2`, Python looks for that module in the same folder as the script `script_1.py` where that import happens.

