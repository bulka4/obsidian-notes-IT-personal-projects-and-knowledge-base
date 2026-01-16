Tags: [[__Machine_Learning_Engineering]]

# Introduction
HTTP transport turns our MCP server into a web service accessible via a URL. We start that server once, it runs all the time until we stop it, and it can handle many requests.

This transport uses the Streamable HTTP protocol, which allows clients to connect over the network. Unlike STDIO where each client gets its own process, an HTTP server can handle multiple clients simultaneously.

The Streamable HTTP protocol provides full bidirectional communication between client and server, supporting all MCP operations including streaming responses. This makes it the recommended choice for network-based deployments

We create a HTTP Transport by providing those parameters to the run() function:
```python
mcp.run(transport="http", host="127.0.0.1", port=8000)
```

#MLEngineering  