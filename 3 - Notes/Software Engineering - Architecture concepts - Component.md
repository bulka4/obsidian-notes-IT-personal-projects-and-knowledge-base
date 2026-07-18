Tags: [[_Software_Engineering]]
#SoftwareEngineering 

# Introduction
Component is a larger deployable or replaceable part. It can be:
- An application
- A group of classes / modules ([[Software Engineering - Architecture concepts - Module|link]])

A component is a unit of software that hides its internal implementation and exposes an interface to other parts of the system.

That interface are for example functions / REST endpoints that other programs can use. Other parts of the system interact only through the interface.

For example:
```
Order Component

Public interface:
    create_order()
    cancel_order()
    get_order()

Internal:
    Order class
    OrderItem class
    Database logic
    Validation rules
```
