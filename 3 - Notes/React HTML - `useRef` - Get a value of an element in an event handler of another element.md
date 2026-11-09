Tags: [[__Frontend_engineering]] [[_React]]
#Frontend #React 

# Introduction
To get data of one HTML element in an event handler of another HTML element ([[HTML - Get a value of an element in an event handler of another element|link]]), for example get input data in an event handler of a button, we can use a few patterns:
# Using `useRef`
```javascript
const inputRef = useRef<HTMLInputElement>(null);

function handleAdd() {
    const value = inputRef.current?.value;
    console.log(value);
}

return (
    <>
        <input ref={inputRef} type="text" />
        <button onClick={handleAdd}>Add task</button>
    </>
);
```
# Using `useState`
Using `useState` hook ([[React - useState hook|link]]):
```javascript
const [value, setValue] = useState("");

function handleAdd() {
    console.log(value);
}

return (
    <>
        <input
            type="text"
            value={value}
            onChange={(event) => setValue(event.target.value)}
        />
        <button onClick={handleAdd}>Add task</button>
    </>
);
```