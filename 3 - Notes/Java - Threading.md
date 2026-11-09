Tags: [[_Java]] [[__Programming_languages]]
#Java #ProgrammingLanguages 

# Introduction
A Java application normally starts with at least one thread ([[Software Engineering - Threads|link]]): the main thread.

For example:
```java
public class Main {
    public static void main(String[] args) {
        System.out.println("Hello");
    }
}
```

When you run this program:
1. The JVM starts.    
2. It creates the main thread.    
3. The main thread executes the `main()` method.    
4. When the method finishes and no other non-daemon threads remain, the application can terminate.    

A thread has its own execution stack, but threads within the same process share the process's memory, including objects in the heap.
# What is multithreading?
Multithreading means running multiple threads within the same application.

For example, imagine a backend application that needs to:
- Process an HTTP request.    
- Read data from a database.    
- Write information to a log file.    

These operations might be handled by different threads, allowing work to progress concurrently.

There are two important concepts:
- Concurrency: Multiple tasks make progress during overlapping periods. They don't necessarily execute at exactly the same time.    
- Parallelism: Multiple tasks actually execute simultaneously, typically on different CPU cores.    

Multithreading can provide concurrency and, depending on the hardware and runtime, parallelism.
# Why to create multiple threads
- each thread can run on a different cpu and perform their tasks in parallel
	- Without managing threads directly we can also use multiple CPUs at the same time, but by managing threads directly, we have more control over it.
- with multiple threads we can achieve concurrency in situations when we can't obtain it with async functions
# Multiple threads vs async functions to obtain concurrency
We can use both creating multiple threads and async functions to obtain concurrency (stop progressing with one task and continue progressing with another task).

With multiple threads we can achieve concurrency in situations when we can't obtain it with async functions.

Async functions can pause execution only at moments declared in code (typically using `await`), when it waits for something (e.g. to load data from a database).

For threads, there are more options for when to stop one thread and continue progressing with another one. The OS scheduler decides which thread gets CPU time and when to switch to another thread (described below in the "How to stop one thread and start another one" section).
## Isolating blocking operations
Imagine your application uses a third-party library that performs blocking operations.

You cannot easily change that library to use asynchronous I/O.

You can isolate its operations in a dedicated thread pool:

```
ExecutorService blockingPool =
    Executors.newFixedThreadPool(5);

Future<String> future = blockingPool.submit(() -> {
    return legacyLibrary.performOperation();
});
```

This prevents those blocking operations from consuming threads needed for other application work.
# How to stop one thread and start another one
## Time slices
The OS scheduler might allocate a small time interval (a time slice, e.g. `t` seconds) to each thread so all threads run in turns, each for `t` sec. 

When Thread A's time slice expires, the OS can suspend it and schedule Thread B.
## Priority-based scheduling
Threads can have different priorities. For example:

|Thread|Priority|
|---|---|
|Thread A|High|
|Thread B|Normal|
|Thread C|Low|

- If Thread A becomes runnable while Thread C is executing, the scheduler may preempt Thread C and schedule Thread A.
- This is called priority-based preemptive scheduling.
- The exact behavior depends on the operating system and scheduling policy.
## Yielding voluntarily
A thread can explicitly indicate that it is willing to give other threads an opportunity to execute.

In Java:
```Java
Thread.yield();
```

This is a hint to the scheduler that the current thread is willing to yield its remaining CPU time.

However, the OS doesn't have to honor it. Another thread might not run at all.

This is different from `sleep()`:
```Java
Thread.sleep(1000);
```

Here, the thread becomes temporarily unavailable for execution for approximately one second.
## Interrupts and events
Hardware and software events can also cause execution to enter the operating system.

For example:
- A network packet arrives.    
- A disk operation completes.    
- A hardware device signals that it has finished an operation.    
- A timer fires.    

The OS handles the event and may wake up threads that were waiting for it.

The scheduler can then choose a newly runnable thread, potentially preempting the currently executing one.
# Creating threads in Java
There are several ways to execute work in another thread.
## 3.1. Extending the Thread class
```java
class MyThread extends Thread {
    @Override
    public void run() {
        System.out.println("Running in another thread");
    }
}
```

Usage:
```java
MyThread thread = new MyThread();

thread.start();
```

Important distinction:
- `run()` executes the method directly on the current thread.    
- `start()` starts a new thread, which then executes `run()`.    

For example:
```java
thread.run();   // No new thread
thread.start(); // New thread
```
## 3.2. Implementing Runnable
A more flexible approach is implementing `Runnable`.
```java
class MyTask implements Runnable {

    @Override
    public void run() {
        System.out.println("Task executing");
    }
}
```

Usage:
```java
Thread thread = new Thread(new MyTask());

thread.start();
```

You can also use a lambda because `Runnable` is a functional interface:
```java
Thread thread = new Thread(() -> {
    System.out.println("Task executing");
});

thread.start();
```

The important distinction is that `Runnable` represents the work, whereas `Thread` represents the thread that executes it.
# 4. Thread lifecycle
A Java thread can be in several states:

|State|Meaning|
|---|---|
|`NEW`|Created but not started|
|`RUNNABLE`|Running or ready to run|
|`BLOCKED`|Waiting to acquire a monitor lock|
|`WAITING`|Waiting indefinitely for another thread's action|
|`TIMED_WAITING`|Waiting for a specified period|
|`TERMINATED`|Execution has finished|

For example:
```java
Thread thread = new Thread(() -> {
    System.out.println("Working...");
});

System.out.println(thread.getState()); // NEW

thread.start();

System.out.println(thread.getState()); // Could be RUNNABLE or TERMINATED
```

The state you observe depends on when you check it because execution happens concurrently.
# 5. Waiting for another thread: `join()`
Sometimes you want one thread to wait until another thread finishes.

You can use `join()`:
```java
Thread thread = new Thread(() -> {
    System.out.println("Task started");
});

thread.start();

try {
    thread.join();
} catch (InterruptedException e) {
    Thread.currentThread().interrupt();
}

System.out.println("Task finished");
```

The main thread waits at `join()` until the other thread terminates.

Without `join()`, the main thread could continue immediately without waiting for the task.
# 6. Thread safety and race conditions
This is one of the most important topics in multithreading.

Remember that threads share memory. This means multiple threads can access and modify the same objects.

Consider:
```java
class Counter {
    int count = 0;

    void increment() {
        count++;
    }
}
```

Now imagine two threads execute:
```java
Counter counter = new Counter();

Thread t1 = new Thread(() -> {
    for (int i = 0; i < 100000; i++) {
        counter.increment();
    }
});

Thread t2 = new Thread(() -> {
    for (int i = 0; i < 100000; i++) {
        counter.increment();
    }
});

t1.start();
t2.start();

t1.join();
t2.join();

System.out.println(counter.count);
```

You might expect `200000`, but the result can be lower.

Why?

Because `count++` is not one indivisible operation. Conceptually, it involves:
1. Reading the current value.    
2. Adding one.    
3. Writing the new value.    

Two threads can interfere with each other.

For example:
- thread A reads 10, thread B read 10
- thread A calculates 11, thread B calculates 11
- thread A writes 11, thread B writes 11

This causes an incorrect result 11, while the correct one is 12.
## Synchronization with `synchronized`
One way to prevent this problem is using `synchronized`:
```java
class Counter {
    int count = 0;

    synchronized void increment() {
        count++;
    }
}
```

Now only one thread at a time can execute a synchronized method on the same `Counter` instance.

The other thread must wait until the lock is released.

You can also synchronize a block:
```java
synchronized (this) {
    count++;
}
```

This is called mutual exclusion: only one thread can enter the protected section at a time for a given lock.
## 6.2. Other concurrency tools
Java provides several other mechanisms:

|Mechanism|Purpose|
|---|---|
|`synchronized`|Mutual exclusion and visibility guarantees|
|`volatile`|Visibility of changes between threads; does not make compound operations atomic|
|`Lock`|More flexible locking mechanisms|
|`AtomicInteger`|Atomic operations on integer values|
|`ConcurrentHashMap`|Thread-safe map|
|`Semaphore`|Limits how many threads can access a resource simultaneously|
|`CountDownLatch`|Makes threads wait until a number of operations are completed|

For example, you can solve the counter problem using `AtomicInteger`:
```java
AtomicInteger counter = new AtomicInteger(0);

counter.incrementAndGet();
```

The increment is atomic, so concurrent calls won't lose updates.
# 7. Thread pools and ExecutorService
In real applications, you generally don't want to create a new thread manually for every task.

Imagine a backend receiving 1,000 HTTP requests. Creating 1,000 threads might consume too many resources.

Instead, Java provides thread pools.

A thread pool maintains a collection of reusable threads that execute submitted tasks.

You can use `ExecutorService`:
```java
import java.util.concurrent.ExecutorService;
import java.util.concurrent.Executors;

public class Main {
    public static void main(String[] args) {

        ExecutorService executor =
                Executors.newFixedThreadPool(3);

        executor.submit(() -> {
            System.out.println("Task 1");
        });

        executor.submit(() -> {
            System.out.println("Task 2");
        });

        executor.submit(() -> {
            System.out.println("Task 3");
        });

        executor.shutdown();
    }
}
```

Here:
- We create a pool with 3 worker threads.    
- We submit 3 tasks.    
- The executor assigns tasks to available threads.    
- `shutdown()` stops accepting new tasks and lets submitted tasks finish.    

You don't need to manage individual threads yourself.

There are also other executor types, including `newSingleThreadExecutor()` and `newCachedThreadPool()`. Modern Java also supports virtual-thread-per-task executors.
# 8. Deadlocks
[[Software Engineering - Concurrency - Deadlocks]]
Another important multithreading problem is a deadlock.

A deadlock happens when threads wait indefinitely for resources held by each other.

Imagine:
- Thread A holds Lock 1 and waits for Lock 2.    
- Thread B holds Lock 2 and waits for Lock 1.    

Neither thread can proceed.

This is different from a race condition:
- Race condition: the result depends on the timing of operations.    
- Deadlock: threads become stuck waiting for each other.    

A common way to prevent deadlocks is to acquire locks in a consistent order.
# Interruption and stopping threads
Sometimes you need to request that a running thread stop its work.

Java provides interruption:
```java
Thread thread = new Thread(() -> {
    while (!Thread.currentThread().isInterrupted()) {
        // Do some work
    }
});

thread.start();

thread.interrupt();
```

`interrupt()` doesn't forcibly terminate the thread. It sets an interruption flag, which the thread can check and respond to.

If a thread is blocked in certain methods such as `sleep()` or `wait()`, interruption causes an `InterruptedException`.

This is important for implementing graceful cancellation.