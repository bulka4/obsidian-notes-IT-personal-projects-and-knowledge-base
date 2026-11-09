Tags: [[_JavaScript]] [[__Programming_languages]]
#JavaScript #ProgrammingLanguages 

# Introduction
To add or overwrite a property of an object, we can use this syntax:
```javascript
const task = { id: 1, title: "Learn React", status: "todo" };
const status = "completed"
// below command will change the "status" property of the "task" object
// into "completed"
{
	...task,
    status: status
}

// shorter version for the same change:
{...task, status}
```
