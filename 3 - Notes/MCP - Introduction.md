Tags: [[__Machine_Learning_Engineering]]

# Introduction
Official documentation about MCP: [modelcontextprotocol.io](https://modelcontextprotocol.io/docs/getting-started/intro).

MCP is a protocol which enables one app to use tools (functions) provided by another app. It is commonly used to enable LLMs to use different tools.

There are two components of MCP:
- MCP server ([[MCP server|link]]) – App where we define different tools which can be used. It is a long-running service that listens to requests and sends back tools' outputs as a response.
- MCP client ([[MCP client|link]]) – App which is using tools from a MCP server

In this document we will focus on FastMCP.

FastMCP is an official Python SDK for working with MCP: [gofastmcp.com](https://gofastmcp.com/getting-started/welcome). It makes it easy to create a MCP server and client in Python.
# Example
For example, on the MCP server we can define a tool like that:
```python
mcp = FastMCP("MyMCPServer")

@mcp.tool()
def add(a, b):
	return a + b
		
# ----- Run Server -----
if __name__ == "__main__":
    # Start the MCP server using the HTTP Transport. This will enable clients to connect over HTTP.
    mcp.run(
        transport="http"
        ,host="0.0.0.0"
        ,port=8000
    )
```

and in the MCP client we can use that tool:
```python
async def mcp_add(a, b):
	# Connect to the MCP server using HTTP Transport
	transport = StreamableHttpTransport(url=mcp_server_url)
	client = Client(transport)

	async with client:
		result = await client.call_tool("add", {"a": a, "b": b})
```

#MLEngineering 