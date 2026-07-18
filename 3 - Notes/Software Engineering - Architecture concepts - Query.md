Tags: [[_Software_Engineering]]
#SoftwareEngineering 

# Introduction
Query is a data object representing a request to read data. It contains the parameters needed to perform the lookup.

Example:
```python
class GetTableQuery:
    def __init__(self, table_id):
        self.table_id = table_id
```