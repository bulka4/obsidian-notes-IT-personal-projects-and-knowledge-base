Tags: [[__Frontend_engineering]] [[_HTML]]
#Frontend #HTML 

# Introduction
To get data of one HTML element in an event handler of another HTML element, for example get input data in an event handler of a button, we can use a few patterns:
# Using `id` (plain JavaScript)
```javascript
<input type="text" id="taskInput" />

<button onclick="handleAdd()">Add task</button>

<script>
    function handleAdd() {
        const value = document.getElementById("taskInput").value;
        console.log(value);
    }
</script>
```
# React
In React we can use additional patterns like described here - [[React HTML - `useRef` - Get a value of an element in an event handler of another element]].