Tags: [[__Machine_Learning_Engineering]]

# Introduction
Instead of creating a MCP server with tools and using them in other Python apps, we can create normal functions in one repository and use them in multiple Python apps from other repositories by installing those functions using pip and importing them in scripts.

Below are benefits of using MCP instead of creating normal Python functions:
- Python functions can’t be used by apps written in other languages than Python (or it’s very difficult to do)
- When we change functions we need to redeploy apps which uses those functions
- MCP provides additional functionalities, for example:
	- List all the available tools
	- Get schema of a given tool, i.e. a JSON describing this tool. It provides information such as:
		- Tool name
		- Tool description
		- Available parameters and their type
		- Which parameters are required

· MCP is a standard and there is more and more tools which are MCP compatible and can be used together with our own MCP server or client.

#MLEngineering 