Tags: [[__Full_Stack_Engineering]]
#FullStackEngineering  

# Introduction
Frontend talks to a backend by running JavaScript code in a browser that makes HTTP requests to a HTTP server.

That JavaScript code can be inside of a HTML code:
```html
<!DOCTYPE html>
<html>
<body>
    <button onclick="loadUsers()">Load users</button>

    <script>
        async function loadUsers() {
            const response = await fetch(
                'https://api.example.com/users'
            );

            const users = await response.json();

            console.log(users);
        }
    </script>
</body>
</html>
```

or it can be in a separate file that is linked to HTML:
```html
<button id="load">Load users</button>
<script src="app.js"></script>
```

```javascript
document.getElementById('load').addEventListener('click', async () => {
    const response = await fetch('https://api.example.com/users');
    const users = await response.json();

    console.log(users);
});
```

JavaScript can be triggered by user action (e.g. clicking on a button) or automatically (e.g. when page loads or regularly over time).
# React, Vue, Angular, etc.
These frameworks don't change the underlying mechanism. They provide abstractions for organizing and executing JavaScript.

For example, in React we define JavaScript code that defines what HTML code to display:
```javascript
function Users() {
    const [users, setUsers] = useState([]);

    async function loadUsers() {
        const response = await fetch('/api/users');
        const data = await response.json();

        setUsers(data);
    }

    return (
        <div>
            <button onClick={loadUsers}>Load users</button>
            {users.map(user => <p key={user.id}>{user.name}</p>)}
        </div>
    );
}
```
# HTML can also trigger HTTP requests without custom JavaScript
For example:
```javascript
<form action="/api/users" method="POST">
    <input name="username">
    <button type="submit">Create user</button>
</form>
```
