Tags: [[_Software_Engineering]]
#SoftwareEngineering 

# Introduction
Service is a standalone application/component. It provides some functionality through an interface (functions, classes).

Service can mean different things, below are different examples.
# 1. Application/domain service (DDD / layered architecture)
A service is a **class that performs an operation that does not naturally belong to an entity**.

Example:
```
Order Aggregate
    |
    v
OrderService
```

Suppose placing an order requires:
- validating inventory
- creating an order
- charging payment
- sending a notification

This workflow does not belong inside `Order` itself.

So you create a service:
```
class OrderService:

    def place_order(self, customer_id, items):
        self.inventory.reserve(items)

        order = Order(customer_id)
        order.add_items(items)

        self.payment.charge(order)

        self.repository.save(order)
```

The `Order` entity still owns its rules:
```
class Order:

    def add_item(self, item):
        if self.status == "SHIPPED":
            raise Exception()

        self.items.append(item)
```

The service coordinates multiple objects.

A useful rule:
- **Entity/Aggregate** → owns business rules about itself
- **Service** → coordinates actions involving multiple objects
# 2. Infrastructure service
A service can also be a technical capability:

Examples:
```
EmailService
PaymentGateway
FileStorageService
CacheService
```

Example:
```
class EmailService:

    def send_email(self, recipient, message):
        smtp.send(...)
```

The rest of the application does not care whether email is sent using:

- SMTP
- SendGrid
- AWS SES

It only uses the service interface.
# 3. Microservice
In distributed systems, a service often means a **separately deployed application**.

Example:
```
E-commerce system

User Service
    |
Order Service
    |
Payment Service
    |
Notification Service
```

Each service:
- runs independently
- has its own deployment
- often owns its own database
- communicates through APIs/events
# Relationship with layers/components
A typical architecture:
```
Application
│
├── Presentation Layer
│   └── Controllers
│
├── Application Layer
│   └── Services
│       └── OrderService
│
├── Domain Layer
│   └── Aggregates
│       └── Order
│
└── Infrastructure Layer
    └── Services
        └── EmailService
```

So:
- **Layer** = organization by responsibility
- **Component** = independent/cohesive part of the system
- **Service** = a component that provides functionality through an interface (often "does something")
- **Entity/Aggregate** = objects that contain business state and rules