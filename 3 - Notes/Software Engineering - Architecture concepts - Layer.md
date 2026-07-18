Tags: [[_Software_Engineering]]
#SoftwareEngineering 

# Introduction
Layer:
- Is a group of responsibilities
- Can consist of components ([[Software Engineering - Architecture concepts - Component|link]]), modules ([[Software Engineering - Architecture concepts - Module|link]]), packages or classes
- Each layer has a specific purpose and usually depends only on layers below it

For example, in a large application:
```
E-commerce System
│
├── Presentation Layer
│   ├── Web API Component
│   ├── Admin UI Component
│   └── CLI Component
│
├── Application Layer
│   ├── Order Service Component
│   ├── Payment Service Component
│   └── User Service Component
│
├── Domain Layer
│   ├── Order Component
│   ├── Payment Component
│   └── Customer Component
│
└── Infrastructure Layer
    ├── Database Component
    ├── Message Broker Component
    └── External API Component
```
Here:
- **Layers** organize by _type of responsibility_.
    - "Presentation" = dealing with users
    - "Domain" = business rules
    - "Infrastructure" = technical details
- **Components** organize by _cohesive functionality_.
    - "Order component"
    - "Payment component"
    - "Database component"
- **Modules/packages** organize the code.

So the relationship is often:
```
System
 └── Layers
      └── Components
           └── Modules
                └── Classes
```