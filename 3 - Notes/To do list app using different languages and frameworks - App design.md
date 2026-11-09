Tags: [[__My_projects]]
#MyProjects 

# Data structures
Task:
```typescript
export type TaskStatus = "todo" | "in_progress" | "done";

export interface Task {
    id: number;
    title: string;
    status: TaskStatus;
}
```
# Components
- `App`
- `TaskList`
- `TaskItem`
- `Login`
## States
- In the App component:
	- `IsLoggedIn` - indicating whether or not the user is logged in
	- `tasks` - list of tasks
- In the `TaskList` component:
	- `newTask` - name of a new task to add to the list