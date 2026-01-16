Tags: [[__Machine_Learning_Engineering]]

# Introduction
MCP server is an app where we define tools which can be used later on by other apps (like accessing a database or using different functions). For example:
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

It is similar to Rest API. It is a long running program (it runs all the time until we stop it) and when other app (a MCP client) sends a request, it sends a response.

In a request we tell what tool we want to use and send parameters for this tool.

As a response we receive an output from this tool for those parameters.

Transport protocols determine how clients interact with the server. There are different types, for example:
- STDIO Transport - [[MCP server - STDIO Transport|link]]
- HTTP Transport - [[MCP server - HTTP Transport|link]]

#MLEngineering 