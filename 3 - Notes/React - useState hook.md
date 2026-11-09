Tags: [[__Frontend_engineering]] [[_React]]
#Frontend #React 

# Introduction
`useState` is a React Hook that allows a component to store information (state) and update it.

It returns an array containing two elements:
```javascript
const [email, setEmail] = useState(default_value);
```
1. `email` – the current state value.
2. `setEmail` – a state updater function - used to update that value.

Initially, `email` is set up to the default value defined by the argument `default_value`.

So writing:
```javascript
const [email, setEmail] = useState("");
```

 works something like:
```javascript
let email = "";

function setEmail(newValue) {
    email = newValue;
}
```
# Updating state and re-rendering UI
When we update state using `setEmail`, React re-renders the component ([[React - Components and elements|link]]) (re-runs the component function) which contains this state, and that updates UI so it reflects the new value.
# Argument for the state updater function (`setEmail`)
For the state updater function (`setEmail`), we can use as an argument:
- A new state value
- A function that receives the previous state and returns the new state

For example:
- Using `setEmail("email@test")` sets up `email = email@test`
- When `email = email@test`, then using `setEmail((email) => email.toUpperCase())` sets up `email = EMAIL@TEST`