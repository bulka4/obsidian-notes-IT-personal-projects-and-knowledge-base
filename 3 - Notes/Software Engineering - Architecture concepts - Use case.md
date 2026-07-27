Tags: [[_Software_Engineering]]
#SoftwareEngineering 

# Introduction
Use Case is a user/system action that the application performs. For example:
- Create document
- Answer question
- Train model

Usually a use case orchestrates entities ([[Software Engineering - Architecture concepts - Entity|link]]) (it uses entities' methods) and external systems.
# Entity vs use case
Entity can contain operations and use cases ([[Software Engineering - Architecture concepts - Use case|link]]) are also operations but different than those which belong to entities.

For example, we can have the `Order` entity like this:
```python
class Order:

    def __init__(self, order_id):
        self.id = order_id
        self.status = "PENDING"

    def confirm(self):
        if self.status != "PENDING":
            raise Exception("Cannot confirm order")

        self.status = "CONFIRMED"
```

and a use case can be a class like this:
```python
class ConfirmOrderUseCase:

    def __init__(self, order_repository):
        self.order_repository = order_repository

    def execute(self, order_id):

        order = self.order_repository.get(order_id)

        order.confirm()

        self.order_repository.save(order)
```
## How to distinguish
A good rule to distinguish whether an operation should belong to an entity or whether it should be a use case, is:
- Entity method - Operations that represents a behavior/rule of a business object
- Use case - Operations that represents a goal the application performs by coordinating things

Also, usually a use case orchestrates entities ([[Software Engineering - Architecture concepts - Entity|link]]) (it uses entities' methods) and external systems.