Tags: [[__Frontend_engineering]] [[_React]]
#Frontend #React 

# Introduction
Conditional rendering in React allows us to create a React element ([[React - Components and elements|link]]) only when a specific condition is satisfied. The syntax is this:
```typescript
{tasks.length === 0 && <p>No tasks yet.</p>}
```

here we can use different operators:
- `&&` - if condition on the left hand side is true, evaluate the right side
- `? :` - means "if ... then ... else", for example: 
  ```typescript
	{isLoggedIn ? <p>Welcome!</p> : <p>Please log in.</p>}
  ```
  