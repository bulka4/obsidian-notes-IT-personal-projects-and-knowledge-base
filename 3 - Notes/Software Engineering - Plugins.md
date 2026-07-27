Tags: [[_Software_Engineering]]
#SoftwareEngineering 

# Introduction
A plugin is a piece of software that extends an existing application without requiring changes to the application's core code.

The main idea is:
> Build a stable core system, then allow additional functionality to be added through predefined extension points.

A plugin is usually developed as a separate module/package/library and loaded by the main application.
# Main characteristics of plugins
A component is usually considered a plugin if it has most of these properties:
## 1. Independent development
The plugin can be developed separately.

Example: A company builds a document management system:
```
Document System
      |
      +-- PDF Export Plugin
      +-- Excel Export Plugin
      +-- Google Drive Plugin
```

A different team can create the Google Drive plugin without modifying the document system.
## 2. Independent deployment
You can add/remove/update plugins separately.

Example: A trading platform:
```
Trading Platform

Plugins:
- Stock market connector
- Crypto exchange connector
- Forex connector
```

Adding support for a new exchange does not require releasing the whole platform.
## 3. Extension points
The application defines places where plugins can connect.

Example: We define an interface ([[Software Engineering - Architecture concepts - Interface|link]]) like this:
```python
from abc import ABC, abstractmethod

class ReportExporter(ABC):
    @abstractmethod
    def export(self, report):
        pass
```

The application says:
> "Any plugin implementing this interface can add a new exporter."

Plugins (interface implementations):
```python
class PdfExporter(ReportExporter):
    def export(self, report):
        # generate PDF
        pass


class ExcelExporter(ReportExporter):
    def export(self, report):
        # generate Excel
        pass
```

The core application does not know about PDF or Excel. We choose a plugin by providing it as an argument and then we use it in code. 

In the example below, we provide a plugin to use but we can also not provide any plugin and the code will still work (so it is not like with a dependency injection ([[Software Engineering - Dependency injection|link]]) where we need to provide a dependency to use):
```python
plugins = [PdfExporter()] # or use ExcelExporter or anything else

class Application:
    def __init__(self, plugins=None):
        self.plugins = plugins or []

    def export(self, report):
        for plugin in self.plugins:
            plugin.export(message)
```
# 3. How plugins are discovered
There are several approaches. We can automatically detect all the available plugins and use them in code.
## Compile-time plugins
The application references plugins directly:
```
Application
   |
   +-- PaymentPlugin.dll
```

Simple but less flexible.
## Configuration-based plugins
Example:

`appsettings.json`
```json
{
  "plugins": [
    "StripePlugin",
    "PaypalPlugin"
  ]
}
```

At startup:
```
Read configuration
        ↓
Load listed plugins
        ↓
Register them
```
## Dynamic discovery
The application scans a folder:
```
/application

/app.exe

/plugins
   ├── Stripe.dll
   ├── Paypal.dll
   └── Bitcoin.dll
```

Startup:
```
Search /plugins folder
        ↓
Find classes implementing IPlugin
        ↓
Load them
```

This is how many extensible applications work.
# 4. Plugin lifecycle
A plugin often has a lifecycle:
```
Discover
   ↓
Load
   ↓
Initialize
   ↓
Execute
   ↓
Shutdown
```

Example:
```python
class Plugin(ABC):
    @abstractmethod
    def initialize(self):
        pass

    @abstractmethod
    def shutdown(self):
        pass
```

The application controls the lifecycle.
# Example
For example, in our application we can have:
```python
def load_storage_plugin(name):
    return PLUGINS[name]()
```

and we create plugins like this, using interfaces ([[Software Engineering - Architecture concepts - Interface|link]]):
```python
from abc import ABC, abstractmethod

PLUGINS = {}  
  
def register(name, cls):  
	PLUGINS[name] = cls

# StoragePlugin interface
class StoragePlugin(ABC):
    @abstractmethod
    def save(self, data):
        pass
        
# Interface implementations - AzureStorage and S3Storage
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
# Plugin vs dependency injection
Providing a plugin is about adding a new functionality while dependency injection ([[Software Engineering - Dependency injection|link]]) is about providing a dependency which is required for the application to run.
# Advantages
- Extensibility - Add features without modifying core code.
- Modularity - Large systems are split into smaller pieces.
- Third-party ecosystem - External developers can extend your product.
- Easier maintenance - Core application remains stable.
# Disadvantages
- Complexity - We need:
	- version compatibility
	- plugin APIs
	- lifecycle management
	- security boundaries
- Debugging difficulty - 
- Versioning problems - for example, a plugin expects `Application API v2` while the application provides `API v3`