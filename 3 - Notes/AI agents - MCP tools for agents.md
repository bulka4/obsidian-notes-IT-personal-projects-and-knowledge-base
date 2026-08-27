Tags: [[_AI_agents]]
#AIAgents

# Introduction
MCP ([[_MCP|link]]) can be used to enable LLMs using tools (functions) ([[AI agents - Using tools by an agent|link]]). 

We create a MCP server ([[MCP server and client|link]]) where we define tools to use, and a separate application (MCP client) where we run a LLM which uses tools provided by the MCP server.

A MCP client where we run a LLM, sends a request to the MCP server specifying which tool to use and with which parameters and MCP server performs calculations and sends back a response.

It is similar to for example REST API but it is a standardized way of providing tools to use by other applications optimized for example for providing tools to use by LLMs.
# Why MCP is useful for creating tools for agents
In order to allow LLMs to use tools ([[AI agents - Using tools by an agent|link]]) to help them to generate an answer, we use a workflow like this:
- LLM generates either:
	- A final answer to a question (don't use any tool)
	- or an answer which indicates to use a tool, which one and with which parameters
- Our application executes a tool and feds the result back to LLM
- LLM generates a final response using the tool's result

So what we need is:
- LLM needs to know:
	- What tools are available
	- How those tools work, what are inputs
- Our application needs to know:
	- Which tool to use based on LLM's response, e.g. when LLM says "use a tool: `semantic_search`", our app needs to know which function exactly is the `semantic_search` tool.

So using MCP to create tools to use by LLMs is beneficial ([[MCP - Benefits, use cases and comparison to other approaches|link]]) because MCP standardizes the way how to:
- discover what tools are available
- provide descriptions what different tools do and what is an input for them
- how tools are invoked
- how tool results are structured

Thanks to the fact that it standardizes those functionalities, we don't need to implement them on our own.

Also, MCP allows us to:
- Get schema of a given tool, i.e. a JSON describing this tool. It provides information such as:
	- Tool name
	- Tool description
	- Available parameters and their type
	- Which parameters are required

Another benefit is that there is more and more tools which are MCP compatible and can be used together with our own MCP server or client.
## Example tools
Using MCP, we can create tools to use for AI agents such as:
- Semantic search ([[_Semantic_search|link]])