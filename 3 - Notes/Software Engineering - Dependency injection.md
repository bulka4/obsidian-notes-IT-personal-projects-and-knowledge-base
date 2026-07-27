Tags: [[_Software_Engineering]]
#SoftwareEngineering 

# Introduction
Dependency Injection (DI) is a software design technique where an object receives its dependencies from the outside instead of creating them itself.

Usually we variables / arguments to specify which dependency to use.

The main idea:
> A class should not create the objects it depends on; those objects should be provided to it.
# Examples
## Dependencies
Different dependencies that we can inject:
- Object of a specific class, for example:
  ```python
	class OrderService:
	    def __init__(self, repository):
		    # We can choose different as the "repository" objects of different 
		    # classes
	        self.repository = repository
  ```
  
  - Configuration, for example:
    ```python
	class ReportService:
	    def __init__(self, config):
	        self.config = config
	        
	# The config variable is our dependency
	config = {
	    "max_rows": 1000,
	    "format": "csv"
	}
	
	service = ReportService(config)
    ```

- A file, for example:
  ```python
	class FileProcessor:
	    def __init__(self, file):
	        self.file = file
	        
	file = open("data.csv")
	
	processor = FileProcessor(file)
  ```
## Interface implementation
Using dependency injection, we can for example provide a specific implementation of an interface ([[Software Engineering - Architecture concepts - Interface|link]]).

So we define an interface like this:
```python
class PaymentGateway:
    def pay(self, amount):
        pass
```

we use it as a dependency in the application:
```python
class OrderService:
    def __init__(self, payment_gateway: PaymentGateway):
        self.payment_gateway = payment_gateway

    def checkout(self, amount):
        self.payment_gateway.pay(amount)
```

and as a dependency injection, we create a class that defines a specific logic for its methods:
```python
class PaypalPayment(PaymentGateway):
    def pay(self, amount):
        # call PayPal API
        pass
```

and use that class (inject a dependency):
```python
order_service = OrderService(payment_gateway=PaypalPayment())
```
# Why to use it
- Easier testing - We can replace a real dependency with a fake one for testing ([[Software Engineering - Test doubles|link]])
- Lower coupling and easier changes - We can use different dependencies without changing the service's code.
# Types of dependency injection
## 1. Constructor injection (most common)
Dependencies are passed through the constructor.
```python
class Service:
    def __init__(self, logger):
        self.logger = logger
```
## 2. Setter injection
Dependencies are assigned after object creation.
```python
service.set_logger(logger)
```
## 3. Method injection
Dependency is passed only to a specific method.
```python
service.process(data, logger)
```
# Plugin vs dependency injection
Providing a plugin ([[Software Engineering - Plugins|link]]) is about adding a new functionality while dependency injection is about providing a dependency which is required for the application to run.