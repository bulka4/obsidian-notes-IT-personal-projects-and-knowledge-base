Tags: [[_Software_Engineering]]
#SoftwareEngineering 

# Introduction
Command is a data object representing a request to do something. it contains information needed to satisfy a request.

Example:
```python
# name and description will be used in a request for creating a table
class CreateTableCommand:
    def __init__(self, name, description):
        self.name = name
        self.description = description
```
