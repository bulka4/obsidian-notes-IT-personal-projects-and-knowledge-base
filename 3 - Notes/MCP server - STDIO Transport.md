Tags: [[__Machine_Learning_Engineering]]

# Introduction
This transport communicates through standard input and output streams.

With STDIO transport, the client spawns a new server process for each session and manages its lifecycle. The server reads MCP messages from stdin and writes responses to stdout. This is why STDIO servers don’t stay running - they’re started on-demand by the client.

This is the default Transport type which is chose when we use run() function without parameters.

#MLEngineering  