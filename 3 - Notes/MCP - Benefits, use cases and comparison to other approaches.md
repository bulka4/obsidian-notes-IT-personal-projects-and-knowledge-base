Tags: [[__Machine_Learning_Engineering]]

# Benefits and functionalities
MCP standardizes the way how to:
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
# Use cases
One of the main applications on MCP is to provide tools to use for LLMs ([[AI agents - MCP tools for agents|link]]).
# MCP vs REST API
Instead of MCP we could use REST API to allow other applications use our functions. 

Everything what we can do using MCP we can also do using REST API but MCP provides a specific set of functionalities which is a standard for exposing tools to AI agents to use.

If we decide to use REST API, we would need to design on our own:
- Tool discovery
	- design how LLMs learn about what tools are available
- Tool descriptions
	- design how LLMs learn about what different tools do
- Tool invocation
	- design how to choose a right tool to use based on LLM's response
	- for example when LLM responses "use a semantic search tool", we need to know that the "semantic search tool" means making a `POST /semantic-search` API call
- Tool result structure
	- design how the tool's result looks like or how to transform it so it can be presented to LLM. 
	- Although LLM should be able to understand any kind of result, not necessarily in the MCP format.
# MCP vs normal Python functions
Instead of creating a MCP server with tools and using them in other Python apps, we can create normal functions in one repository and use them in multiple Python apps from other repositories by installing those functions using pip and importing them in scripts.

But using MCP instead of creating normal Python functions has some benefits, for example:
- Python functions can’t be used by apps written in other languages than Python (or it’s very difficult to do)
- When we change functions we need to redeploy apps which uses those functions
- MCP provides additional functionalities, for example:
	- Tools discovery
	- Getting schema of a given tool
- MCP is a standard and there is more and more tools which are MCP compatible and can be used together with our own MCP server or client.

#MLEngineering 