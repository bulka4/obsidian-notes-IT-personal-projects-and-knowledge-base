Tags: [[__Frontend_engineering]] [[_EJS]]
#Frontend #EJS  

# Introduction
EJS is used to insert values of variables into HTML before displaying it in a browser. It can be used together with Express ([[_Express|link]]).

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