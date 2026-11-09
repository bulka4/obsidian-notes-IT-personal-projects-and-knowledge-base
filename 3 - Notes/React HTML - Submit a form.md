Tags: [[__Frontend_engineering]] [[_React]]
#Frontend #React 

# Introduction
In React, submitting a form ([[HTML - Submit a form|link]]) has the following syntax:
```javascript
<form onSubmit={handleSubmit}>
	{/* Input for providing an email */}
	<input
		type="email"
		placeholder="Email"
		value={email}
	/>

	{/* Input for providing a password */}
	<input
		type="password"
		placeholder="Password"
		value={password}
	/>

	<button type="submit">Login</button>
</form>
```
# Event handler - `onSubmit`
We can use the `onSubmit` event handler to run JavaScript code when submitting a form:
```typescript
const [email, setEmail] = useState("");
const [password, setPassword] = useState("");

function handleSubmit(event: React.FormEvent<HTMLFormElement>) {
	event.preventDefault();

	// We can use here the "email" and "password" state variables
}

<form onSubmit={handleSubmit}>
	{/* Input for providing an email */}
	<input
		type="email"
		placeholder="Email"
		value={email}
		// Set up a value of the "email" state
		onChange={(event) => setEmail(event.target.value)}
		required
	/>

	{/* Input for providing a password */}
	<input
		type="password"
		placeholder="Password"
		value={password}
		// Set up a value of the "password" state
		onChange={(event) => setPassword(event.target.value)}
		required
	/>

	<button type="submit">Login</button>
</form>
```
## Get input data for the event handler `onsubmit`
To access input values in the `handleSubmit` function, we can use the `event.currentTarget` attribute and `FormData` API like in standard HTML (explained here - [[HTML - Submit a form|link]]) or the `useState` hook ([[React - useState hook|link]]) like shown in the example above.