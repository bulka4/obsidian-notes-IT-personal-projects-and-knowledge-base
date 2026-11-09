Tags: [[__Frontend_engineering]] [[_React]]
#Frontend #React 

# Introduction
A component is a function that returns a JSX element, for example:
```typescript
// Component: a function that returns a JSX element
function Greeting() {
  return <h1>Hello!</h1>;
}

// JSX element
const element = <Greeting />;
```
# Transferring JSX into DOM
JSX element returned by a component is then transformed into a React element which is used by React to update the browser's DOM like explained here - [[React - Transferring JSX into DOM]].
# Component input arguments
We can define input argument in a few ways:

Using an interface:
```typescript
interface UserProps {
    name: string;
    age: number;
}

function User({ name, age }: UserProps) {
    return <p>{name}, {age}</p>;
}
```

Using a type alias:
```typescript
type UserProps = {
    name: string;
    age: number;
};

function User({ name, age }: UserProps) {
    return <p>{name}, {age}</p>;
}
```

Defining types directly in the function:
```typescript
function User({ name, age }: { name: string; age: number }) {
    return <p>{name}, {age}</p>;
}
```