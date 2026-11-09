Tags: [[__Frontend_engineering]] [[_HTML]]
#Frontend #HTML 

# Introduction
The HTML `<form>` element is used to collect user input and submit it, usually to a backend.

For example, a login form might collect an email and password and send them to a server.
# `action` & `method` - make a HTTP request
We can use this syntax to make a HTTP call when submitting a form:
```HTML
<form action="/login" method="POST">
    <label for="email">Email:</label>
    <input type="email" id="email" name="email">

    <label for="password">Password:</label>
    <input type="password" id="password" name="password">

    <button type="submit">Log in</button>
</form>
```

here:
- `action="/login"` specifies the URL where the form data should be sent.
- `method="POST"` specifies the HTTP method used to submit the data.
- When the user clicks Log in, the browser automatically sends an HTTP POST request to `/login`, containing the form data in the request's body, for example: `email=john@example.com&password=123456`
# Event handler `onsubmit` - execute JavaScript code
We can use the `onsubmit` event handler attribute to define what JavaScript code is executed when a form is submitted:
```html
<form onsubmit="handleSubmit(event)">
    <input type="email" name="email">
    <button type="submit">Submit</button>
</form>

<script>
    function handleSubmit(event) {
        event.preventDefault();

        console.log("Form submitted!");
    }
</script>
```
## Get input data for the event handler `onsubmit`
To get data from the `<input/>` element in the event handler `onsubmit`, we can use the `FormData` API:
```javascript
<form onsubmit="handleSubmit(event)">
    <input type="email" name="email">
    <button type="submit">Submit</button>
</form>

<script>
    function handleSubmit(event) {
        event.preventDefault();

        const formData = new FormData(event.target);
        const email = formData.get("email");

        console.log(email);
    }
</script>
```
# React
In React, the syntax is described here - [[React HTML - Submit a form]].
# Features (comparison to using `<input/>` outside of a `<form/>`)
When using `<input/>` inside of a `<form/>`, we get:
- Pressing Enter in an appropriate input can also submit the form.
- You can retrieve all form values together using `FormData`.
- HTML validation (e.g. `required`, `type="email"`) is performed automatically before submission.