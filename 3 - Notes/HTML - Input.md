Tags: [[__Frontend_engineering]] [[_HTML]]
#Frontend #HTML 

# Introduction
The HTML `<input>` element is used to collect data from users, for example, email addresses, passwords, names, numbers, etc.

Example:
```typescript
<input
    type="email"
    placeholder="Enter your email"
    value={email}
    onChange={(event) => setEmail(event.target.value)}
    required
/>
```
# Attributes
- `type` - Defines the type of input (text, email, password, number, etc.).
- `value` - Defines the current value displayed in the input.
- `placeholder` - Displays a hint when the input is empty.
- `onChange` - Event handler triggered when the input value changes.
- `required` - Makes the field mandatory when submitting a form.
# `onChange` - the `event` argument
The `event` argument contains information about the event.

The `event.target` property is The HTML element that triggered the event (here, the `input` element containing this `onChange` function). We can access attributes of this HTML element, for example:
- `event.target.type = "email"`
- `event.target.value = {email}`
