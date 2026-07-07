Tags: [[_Python]] [[__Programming_languages]]
#Python #ProgrammingLanguages 

# Introduction
The `dataclass` decorator can be used for creating classes in a special format for storing data:
```python
from dataclasses import dataclass

@dataclass
class User:
    id: int
    name: str
    email: str
    
    def function(x):
	    ...
    
user = User(1, "Alice", "alice@test.com")
print(user.email)
```
# Comparison to a dataframe and dictionary
When we don't need to perform aggregations or filtering, then using data classes is more convenient than dataframe:
```python
user.email
# instead of
user.iloc[i. 'email']
```

It might be also more convenient than dictionary:
```python
# dictionary
config = {
    "storage": "azure",
    "workers": 4
}

config["storage"]

# dataclass
@dataclass
class Config:
    storage: str
    workers: int
    
config.storage
```