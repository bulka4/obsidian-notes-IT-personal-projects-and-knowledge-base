Tags: [[_Software_Engineering]]
#SoftwareEngineering 

# Introduction
The Choreography (event-driven) saga pattern type ([[Software Engineering - Architecture patterns - Saga|link]]) is used in event-driven systems ([[Backend Engineering - Event-driven architecture (EDA)|link]]).

Using this type, when a producer sends a message to a consumer and processing the message by the consumer fails, then:
- Consumer publishes an event about this failure
- Other services reacts to it and perform compensation actions (usually they undo actions they performed before the failure)

So every service subscribes to (looks for) failure events relevant to it and once they appear, the service perform compensation actions.

For example, if we have two services:
- Order Service → create order
- Payment Service → charge card
then:
- Order service sends a message to the Payment service to charge the card after making an order
- Payment service fails, it publishes a failure event
- Order service receives that failure event and cancels order
# Benefits
- Loose coupling between services - Services do not directly call each other. They don't need to know about each others existance.
- No central coordinator - There is no orchestrator that controls the whole workflow, so that is one component less to maintain
- Easy to add new reactions - We can add a new service by subscribing to existing events.
- Good fit for event-driven systems - If our system is already based on events, choreography can feel natural
# Drawbacks
- Workflow logic becomes distributed - The whole process is spread across services. To understand the complete workflow, we need to look at multiple services.
- Harder debugging - When something fails, we may need to trace many events. Finding where the problem happened can be difficult.
- Risk of complex event chains - With many services it becomes harder to understand who reacts to what, what is the order of events, what happens during failures.
- Duplicate event handling - Because messages can be delivered more than once, every service must handle duplicates safely.