Tags: [[_Backend_Engineering]] [[_Kafka]]
#BackendEngineering #Kafka 

# Introduction
Kafka security is about protecting Kafka clusters from unauthorized access and ensuring data is transmitted safely.
# Areas
1. Authentication — "Who are you?"
	- Verifies the identity of clients (producers, consumers, brokers). For example:
		- SSL/TLS certificates ([[Networking - Security - TLS|link]])
		- SASL (username/password, tokens, Kerberos, etc.)
2. Authorization — "What are you allowed to do?" - 
	- Controls what authenticated users/services can access. 
	- Kafka uses ACLs (Access Control Lists) for this.
3. Encryption — "Can others read the data?"
	- Protects data in transit, e.g. using TLS ([[Networking - Security - TLS|link]])
# Related topics
- Authentication (SSL, SASL) - [[Kafka - Authentication (SSL, SASL)|link]] 
- Authorization (ACLs) - [[Kafka - Authorization (ACLs)|link]] 