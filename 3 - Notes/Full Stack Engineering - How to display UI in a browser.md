Tags: [[__Full_Stack_Engineering]]
#FullStackEngineering  

# Introduction
To display UI in a browser we need a HTTP server. It works like that:
- user enters URL in a browser with a DNS name ([[Networking - DNS, domains, hostnames and FQDN|link]]) or IP address of a HTTP server to connect to
- The server responds with an HTML document.
- The browser parses the HTML and requests additional resources referenced by it, such as CSS, JavaScript and images.
- The browser executes JavaScript, applies CSS and renders the UI.

The frontend code that HTTP sends to a browser can consist of:
- Pure HTML, CSS and JavaScript.
- A frontend framework such as React ([[_React|link]]), Vue or Angular, which is typically compiled or bundled into browser-compatible JavaScript.
# How a frontend talks to a backend
[[Full Stack Engineering - How a frontend talks to a backend]]