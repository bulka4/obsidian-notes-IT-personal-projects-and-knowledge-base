Tags: [[_Java]] [[__Programming_languages]] [[_Java_Spring]] [[_Java_Spring_MVC–REST_Controllers]]
#Java #ProgrammingLanguages #JavaSpring  #JavaSpringMVC-RESTControllers 

# Introduction
These annotations tell Spring which HTTP status code to return when the method completes successfully:
```java
@ResponseStatus(HttpStatus.CREATED)
```
and:
```java
@ResponseStatus(HttpStatus.NO_CONTENT)
```
# Example - to do app
For example, in a to-do app where we create tasks to do:
## Creating a task
```java
@PostMapping
@ResponseStatus(HttpStatus.CREATED)
public TaskDtos.TaskResponse createTask(...) {
    return taskService.createTask(request, currentUser);
}
```

`HttpStatus.CREATED` means HTTP `201`.

This is the conventional status code for successfully creating a resource.

The response might look like:
```
HTTP/1.1 201 Created
Content-Type: application/json
```

```json
{
    "id": 123,
    "title": "Learn Spring",
    "status": "TODO"
}
```

### Deleting a task
```java
@DeleteMapping("/{id}")
@ResponseStatus(HttpStatus.NO_CONTENT)
public void deleteTask(...) {
    taskService.deleteTask(id, currentUser);
}
```

`HttpStatus.NO_CONTENT` means HTTP `204`.

It indicates that the operation succeeded but there is no response body.

This makes sense because the client doesn't necessarily need any data after deleting a task.

Without `@ResponseStatus`, Spring would generally return `200 OK` for a successfully completed controller method.