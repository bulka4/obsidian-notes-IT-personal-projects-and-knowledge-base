Tags: [[_Software_Engineering]]
#SoftwareEngineering 

# Introduction
Plugins are classes that can be created and made available to use in applications without changing the application itself.

For example, in our application we can have:
```python
def load_storage_plugin(name):
    return PLUGINS[name]()
```

and we create plugins like this:
```python
from abc import ABC, abstractmethod

PLUGINS = {}  
  
def register(name, cls):  
	PLUGINS[name] = cls

class StoragePlugin(ABC):
    @abstractmethod
    def save(self, data):
        pass
        
class AzureStorage(StoragePlugin):
    def save(self, data):
        ...  
register("azure", AzureStorage)
        
class S3Storage(StoragePlugin):
    def save(self, data):
        ...  
register("s3", S3Storage)
```

After creating a new plugin, we can use it in the application using `load_storage_plugin` without changing the app's code.