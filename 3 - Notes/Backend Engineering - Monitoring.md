Tags: [[_Backend_Engineering]]
#BackendEngineering 

# Introduction
You cannot debug distributed communication without:
- Logs (structured logging)
- Metrics (latency, error rate, throughput)
- Tracing (OpenTelemetry)

Example:  
A single request might travel:  
API Gateway → Auth → User Service → DB → Payment Service  
Tracing shows the full path.
# Related topics
1. Tracing - [[Backend Engineering - Monitoring - Tracing|link]] 
2. Traces vs metrics vs logs - [[Backend Engineering - Monitoring - Traces vs metrics vs logs|link]] 
3. Correlation ID - [[Backend Engineering - Monitoring - Correlation ID|link]] 