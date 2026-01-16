Tags: [[_AI_agents]]
#AIAgents

# Introduction
MCP ([[_MCP|link]]) can be used to enable LLMs using tools (functions) which we define in a separate app. 

That separate app is a long running service which listens to requests from other apps and sends back tools outputs as a response, similarly to Rest API.
## Example use case
We can use a vector database for performing a semantic search and enable querying that database through MCP or Rest API like described in documents below:
- [[Vector databases - Semantic search]]
- [[Serving vector db search – Rest API - MCP]]