Tags: [[__My_projects]]
#MyProjects 

# My code
`App.tsx`:
```typescript
import { useState } from "react";
import type { Task, TaskStatus } from "./types";
import Login from "./components/Login";
import TaskList from "./components/TaskList";

function App() {
    
    // State indicating whether or not the user is logged in
    const [isLoggedIn, setIsLoggedIn] = useState(false);

    // state with a list of tasks
    const [tasks, setTasks] = useState<Task[]>([
        { id: 1, title: "Learn React", status: "todo" },
        { id: 2, title: "Learn TypeScript", status: "in_progress" },
        { id: 3, title: "Build an application", status: "done" }
    ]);

    function addTask(task_title: string) {
        // Add a new task to the "tasks" state
        const task: Task = {
            id: Date.now(),
            title: task_title,
            status: "todo"
        };

        setTasks((previousTasks) => [...previousTasks, task]);
    }

    function removeTask(id: number) {
        // Remove a task from the "tasks" state
        setTasks((previousTasks) =>
            previousTasks.filter((task) => task.id !== id)
        );
    }

    function changeTaskStatus(id: number, status: TaskStatus) {
        // Change the status of the task in the "tasks" state with a specific ID 
        setTasks((previousTasks) =>
            previousTasks.map((task) =>
                task.id === id ? { ...task, status } : task
            )
        );
    }

    if (!isLoggedIn) {
        return <Login onLogin={() => setIsLoggedIn(true)} />;
    }

    return (
        <div className="app-container">
            <header>
                <h1>To-Do App</h1>
                <button onClick={() => setIsLoggedIn(false)}>
                    Logout
                </button>
            </header>

            <TaskList
                tasks={tasks}
                onAdd={addTask}
                onRemove={removeTask}
                onStatusChange={changeTaskStatus}
            />
        </div>
    );
}

export default App;
```

`TaskList.tsx`
```typescript
import { useState } from "react";
import type { Task, TaskStatus } from "../types";
import TaskItem from "./TaskItem";

interface TaskListProps {
    tasks: Task[];
    onAdd: (task_title: string) => void;                        // function for adding a task to the list
    onRemove: (id: number) => void;                             // function for removing a task
    onStatusChange: (id: number, status: TaskStatus) => void;   // function for changing up a task's status
}

function TaskList({
    tasks,
    onAdd,          
    onRemove,       
    onStatusChange  
}: TaskListProps) {

    // state with a name of a new created task
    const [newTask, setNewTask] = useState("");

    function handleAdd() {
        // Execute the onAdd function that will add a task to the list
        if (!newTask.trim()) return;

        onAdd(newTask.trim());
        setNewTask("");
    }

    return (
        <div className="task-list">
            <h2>My Tasks</h2>

            {/* Adding a new task */}
            <div className="add-task">
                {/* Input for a task name */}
                <input
                    type="text"
                    placeholder="Enter a task..."
                    value={newTask}
                    // Set up the entered value as the value of the "newTask" state
                    onChange={(event) => setNewTask(event.target.value)}
                />

                {/* Button for adding a task */}
                <button onClick={handleAdd}>Add task</button>
            </div>

            {/* list all the task items */}
            <div>
                {tasks.map((task) => (
                    <TaskItem
                        key={task.id}
                        task={task}
                        onRemove={onRemove}
                        onStatusChange={onStatusChange}
                    />
                ))}
            </div>

            {tasks.length === 0 && <p>No tasks yet.</p>}
        </div>
    );
}

export default TaskList;
```

`TaskItem.tsx`
```typescript
import type { Task } from "../types";

interface TaskItemProps {
    task: Task;
    onStatusChange: (id: number, status: Task["status"]) => void;   // function for setting up a task's status
    onRemove: (id: number) => void;                                 // function for removing a task
}

function TaskItem({ task, onStatusChange, onRemove }: TaskItemProps) {
    return (
        <div className="task-item">
            <span>{task.title}</span>

            {/* Option for changing a status of a task */}
            <select
                value={task.status}
                // Set up as a new status, the value of the selected option
                onChange={(event) =>
                    onStatusChange(
                        task.id,
                        event.target.value as Task["status"] // value of the selected option
                    )
                }
            >
                <option value="todo">To do</option>
                <option value="in_progress">In progress</option>
                <option value="done">Done</option>
            </select>

            {/* Button for removing an item from the list */}
            <button onClick={() => onRemove(task.id)}>
                Remove
            </button>
        </div>
    );
}

export default TaskItem;
```

`TaskLogin.tsx`
```typescript
import { useState } from "react";

interface LoginProps {
    onLogin: () => void;    // function for logging in
}

function Login({ onLogin }: LoginProps) {
    const [email, setEmail] = useState("");
    const [password, setPassword] = useState("");

    function handleSubmit(event: React.FormEvent<HTMLFormElement>) {
        // Function for logging in when submitting an email and a password
        event.preventDefault();

        if (email.trim() && password.trim()) {
            onLogin();
        }
    }

    return (
        <div className="login-container">
            <h1>To-Do App</h1>

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
        </div>
    );
}

export default Login;
```

`Types.ts`
```typescript
// Define the structure of the task

export type TaskStatus = "todo" | "in_progress" | "done";

export interface Task {
    id: number;
    title: string;
    status: TaskStatus;
}
```

