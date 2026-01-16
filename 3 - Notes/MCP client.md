Tags: [[__Machine_Learning_Engineering]]

# Introduction
MCP client is an app which uses tools defined in a MCP server.

For example here is a code which uses a tool from a MCP server which uses HTTP Transport:
 ```python
async def mcp_add(a, b):
	# Connect to the MCP server using HTTP Transport
	transport = StreamableHttpTransport(url=mcp_server_url)
	client = Client(transport)

	async with client:
		result = await client.call_tool("add", {"a": a, "b": b})
```

#MLEngineering 