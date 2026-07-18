Tags: [[_Python]] [[__Programming_languages]] [[_Software_Engineering]]
#Python #ProgrammingLanguages #SoftwareEngineering 

# Introduction
Profiling is the process of measuring a program's performance to find where time and resources are being spent.

It helps answer questions like:
- Which functions are slow?
- How much time does each function take?
- How much memory is being used?
- Where are bottlenecks?
# Example
```python
import cProfile

cProfile.run("my_function()")
```

Output might show:
```
function        calls    time
process_data    100      5.2s
load_file       1        0.8s
```
# Types
- **CPU profiling** → measures execution time of functions
    - `cProfile`
    - `py-spy`
- **Memory profiling** → finds excessive memory usage
    - `memory_profiler`
    - `tracemalloc`
- **Line profiling** → measures time spent on individual lines