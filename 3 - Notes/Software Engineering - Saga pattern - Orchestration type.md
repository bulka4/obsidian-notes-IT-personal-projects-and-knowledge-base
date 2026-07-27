Tags: [[_Software_Engineering]]
#SoftwareEngineering 

# Introduction
In the orchestration saga pattern type ([[Software Engineering - Architecture patterns - Saga|link]]), a central coordinator `Saga Orchestrator` controls the flow. It tells each service what action to perform and when, and also what compensation actions to perform when a failure occurs.

For example, we could have a flow like this:
- Orchestrator sends command `ChargePayment` to the payment service to charge the customer's card
- Payment service responds that the payment was completed successfully
- Orchestrator sends a command to the inventory service to prepare a product to send to the customer
- Inventory service fails
- Orchestrator decides what compensation actions to perform, e.g. it can tell the payment service to return money
# Common tools to set up orchestrator
## Workflow orchestration engines
- Temporal Technologies
    - Define workflows as code.
    - Handles retries, failures, state persistence, and compensation.
- Camunda
    - Uses BPMN diagrams to model business processes.
    - Good for enterprise workflows.
- Netflix Conductor
    - Designed for orchestrating microservice workflows.
## Message brokers + custom orchestrator
Build our own orchestrator service which talks to multiple services through a message broker ([[Backend Engineering - Event-driven architecture - Message broker|link]]):
```
Orchestrator service
        |
        v
Message broker
        |
        +--> Payment service
        +--> Inventory service
        +--> Shipping service
```

Tools:
- Apache Kafka
- RabbitMQ
- Amazon Simple Queue Service

The orchestrator stores the workflow state and decides the next command.
## Cloud workflow services
- AWS Step Functions
- Azure Logic Apps
- Google Cloud Workflows
# Benefits
- Easier to understand the workflow - because it is defined in one place, the orchestrator
- Easier debugging and monitoring - Because the orchestrator knows the current state, it is easier to understand what happened.
- Better handling of complex workflows - For workflows with many steps, conditions, and failures, the logic is easier to manage in one component.
- Clear ownership of business process - The orchestrator owns the workflow, other services only need to perform their specific operations
# Drawbacks
- More coupling to the orchestrator - Services need to expose operations that the orchestrator can call.
- Orchestrator can become a bottleneck - It can get overloaded and it is a single point of failure
- Additional infrastructure and complexity - we need to maintain the orchestrator, that is one additional component to maintain
