Tags: [[__Frontend_engineering]]
#Frontend 

# Introduction
JSX (JavaScript XML) is a syntax extension for JavaScript that allows us to write HTML-like code inside JavaScript.

It's commonly used with React to describe what the UI should look like.
# Without JSX
You can create a React element ([[React - Components and elements|link]]) using regular JavaScript:
```javascript
const element = React.createElement(
    "h1",
    null,
    "Hello world!"
);
```
# With JSX
The same thing using JSX:
```javascript
const element = <h1>Hello world!</h1>;
```
# JSX with JavaScript
You can also embed JavaScript expressions inside JSX using `{}`:
```javascript
function App() {
    const name = "John";

    return (
        <div>
            <h1>Hello, {name}!</h1>
            <p>Welcome to my application.</p>
        </div>
    );
}
```
# JSX with React components
You can use other React components inside JSX:
```javascript
function Task() {
    return <p>Learn React</p>;
}

function App() {
    return (
        <div>
            <h1>My tasks</h1>
            <Task />
            <Task />
        </div>
    );
}
```

Here, `<Task />` is a React component.
# Compilers
Browsers don't understand JSX directly. We need a compiler to transform JSX/TSX into regular JavaScript that the browser can execute.

For example, when using Vite, we can select to use a compiler.