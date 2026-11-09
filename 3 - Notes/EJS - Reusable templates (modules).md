Tags: [[__Frontend_engineering]] [[_EJS]]
#Frontend #EJS  

# Introduction
With EJS, we can create reusable HTML templates so we can just use a template name instead of all the HTML it contains, something like functions in object oriented programming.

For example, we might have the `header.ejs` template:
```html
<header>
    <h1>My Application</h1>
    <nav>...</nav>
</header>
```

and use it in another file, `index.ejs`:
```html
<body>
    <%- include('header') %>

    <main>
        <h2>Welcome</h2>
    </main>
</body>
```
