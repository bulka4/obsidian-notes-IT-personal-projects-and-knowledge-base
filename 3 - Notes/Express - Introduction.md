Tags: [[__Frontend_engineering]] [[_Express]]
#Frontend #Express  

# Introduction
Express is used with Node.js and it allows for creating HTTP endpoints (routes) ([[Backend Engineering - API endpoint, route and handler|link]]).

It can also send HTML files to a browser to display UI. Those can be either static HTML files or HTML files where we insert values of variables, using e.g. EJS ([[_EJS|link]]).

For example:
```javascript
const express = require('express');

const app = express();

// Configure EJS as the template engine
app.set('view engine', 'ejs');

// Define a route
app.get('/', (req, res) => {
    res.render('index', {
        title: 'My Website',
        username: 'John',
        items: ['Python', 'JavaScript', 'SQL']
    });
});

app.listen(3000, () => {
    console.log('Server running on port 3000');
});
```

```html
<!DOCTYPE html>
<html>
<head>
    <title><%= title %></title>
</head>
<body>

    <h1>Welcome, <%= username %>!</h1>

    <h2>My skills:</h2>

    <ul>
        <% items.forEach(item => { %>
            <li><%= item %></li>
        <% }); %>
    </ul>

</body>
</html>
```