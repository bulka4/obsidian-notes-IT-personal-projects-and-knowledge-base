Tags: [[_Python]] [[__Programming_languages]] [[_Software_Engineering]]
#Python #ProgrammingLanguages #SoftwareEngineering 

# Introduction
**Multiprocessing** is a way to run multiple processes in parallel on different CPU cores, where each process has its own memory space and Python interpreter.
# Example
```python
from multiprocessing import Process

def work():
    print("Working")

p = Process(target=work)
p.start()
p.join()
```

Here:
- `Process` creates a separate process.
- `start()` runs it.
- `join()` waits for it to finish.
# Why use multiprocessing
- Can run multiple processes in parallel using multiple CPU cores.
- Good for CPU-bound tasks (e.g., data processing, simulations, computations).
- Avoids Python's GIL limitation (Global Interpreter Lock).
# Multiprocessing vs multithreading

| |Multiprocessing|Multithreading|
|---|---|---|
|Execution|Separate processes|Threads in one process|
|Memory|Separate|Shared|
|CPU-bound tasks|Good|Limited by GIL in CPython|
|Communication|More complex|Easier|
