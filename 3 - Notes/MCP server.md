Tags: [[__Machine_Learning_Engineering]]

# Introduction
MCP server is an app where we define tools which can be used later on by other apps (like accessing a database or using different functions). For example:
![[2 - Images/MCP - FastMCP/Screenshot 1.png]]

It is similar to Rest API. It is a long running program (it stops when we stop it) and when other app (a MCP client) sends a request, it sends a response.

In a request we tell what tool we want to use and send parameters for this tool.

As a response we receive an output from this tool for those parameters.

Transport protocols determine how clients interact with the server. There are different types, for example:
- STDIO Transport - [[MCP server - STDIO Transport|link]]
- HTTP Transport - [[MCP server - HTTP Transport|link]]

#MLEngineering 