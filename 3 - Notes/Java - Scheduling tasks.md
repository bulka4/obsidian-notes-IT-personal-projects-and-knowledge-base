Tags: [[_Java]] [[__Programming_languages]]
#Java #ProgrammingLanguages 

# Introduction
In Java, TimerTasks are used to execute code at a specific time or repeatedly at scheduled intervals.

They are part of Java's built-in scheduling mechanism and are useful for background tasks such as:
- Periodically checking something.
- Cleaning up temporary files.
- Refreshing cached data.
- Running scheduled operations.
- Executing a task after a delay.

Java provides two related classes:
- `Timer` – manages scheduling and execution.
- `TimerTask` – represents the actual task to execute.
# `TimerTask` - Create a task
`TimerTask` is used to create a task that can we scheduled using the `Timer` class.

`TimerTask` is an abstract class. You create a subclass and implement its `run()` method.
```java
import java.util.TimerTask;

class MyTask extends TimerTask {
    @Override
    public void run() {
        System.out.println("Task executed!");
    }
}
```

Notice that `TimerTask` is a class, not an interface. Therefore, you extend it rather than implement it.
# `Timer` - Scheduling a task
We can use the `Timer` class to schedule a task created using the `TimerTask` class:
```java
import java.util.Timer;

public class Main {
    public static void main(String[] args) {
        Timer timer = new Timer();

        MyTask task = new MyTask();

        timer.schedule(task, 3000);
    }
}
```

The `timer.schedule(task, 3000);` command will run the task after 3 seconds.
# Scheduling repeated execution
You can also execute a task repeatedly.

There are two particularly useful methods.

`schedule()` – fixed delay - start next execution 2 seconds after COMPLETING the previous one:
```java
Timer timer = new Timer();

timer.schedule(new MyTask(), 1000, 2000);
```

Arguments:
1. Task to execute.    
2. Initial delay: 1 second.    
3. Period: 2 seconds.    

`scheduleAtFixedRate()` – fixed rate - start next execution 2 seconds after STARTING the previous one
```java
timer.scheduleAtFixedRate(new MyTask(), 1000, 2000);
```

The difference matters when a task takes longer than expected:
- `schedule()` maintains a delay between finishing one execution and starting the next one.    
- `scheduleAtFixedRate()` maintains a delay between starting every execution 
# Cancelling scheduled tasks
You can cancel an individual task:
```java
MyTask task = new MyTask();

timer.schedule(task, 1000, 2000);

// Cancel this task
task.cancel();
```

Or cancel the entire timer:
```java
timer.cancel();
```

After cancellation, the timer cannot be reused.

You should also remember to cancel timers when they are no longer needed, otherwise their background thread can prevent your application from terminating.
# An important alternative: ScheduledExecutorService
Although `Timer` is useful for learning, modern Java applications generally prefer `ScheduledExecutorService`.

It provides more flexibility and better concurrency management.

For example:
```java
import java.util.concurrent.*;

public class Main {
    public static void main(String[] args) {
        ScheduledExecutorService executor =
            Executors.newScheduledThreadPool(1);

        executor.scheduleAtFixedRate(
            () -> System.out.println("Task executed!"),
            1,
            2,
            TimeUnit.SECONDS
        );

        // Later, when shutting down:
        // executor.shutdown();
    }
}
```

Notice that we can use a lambda here because `scheduleAtFixedRate()` accepts a `Runnable`, which is a functional interface.

Some advantages:
- Can manage multiple threads.    
- Can execute multiple scheduled tasks concurrently.    
- Provides more flexible scheduling.    
- Better suited to concurrent applications.
# Spring Boot
Spring provides its own scheduling functionality.

For example:
```java
@Component
public class MyScheduledTask {

    @Scheduled(fixedRate = 5000)
    public void execute() {
        System.out.println("Task executed!");
    }
}
```

This executes the method every 5 seconds.

You need to enable scheduling using `@EnableScheduling` in your Spring application configuration.

This is particularly useful for backend operations such as periodically refreshing data, processing background jobs, and checking system status.