Tags: [[_JavaScript]] [[__Programming_languages]]
#JavaScript #ProgrammingLanguages 

# Introduction
In JavaScript, we can create functions that generate HTML strings and insert them into HTML elements:
```javascript
function createUserCard(name, email) {
    return `
        <div class="user-card">
            <h2>${name}</h2>
            <p>${email}</p>
        </div>
    `;
}

// find a HTML element with id="users" and insert HTML into it
document.getElementById("users").innerHTML =
    createUserCard("John", "john@example.com");
```

