Tags: [[_Java]] [[__Programming_languages]]
#Java #ProgrammingLanguages 

# Stack memory
- Stack memory contains stack frames.
- The JVM uses a call stack to keep track of method calls.
- Every time a method is called, a new stack frame is created and pushed onto the stack. 
- When the method finishes, its frame is removed.
## Stack frame
A stack frame contains information needed for one particular method invocation, such as:
- Local variables (including reference variables).
- Method parameters.
- Intermediate calculation results.
- Information needed to return from the method.
# Heap memory
Heap memory is memory area typically used for objects.
# Related topics
1. [[Java - Removing a reference variable vs removing an object from a heap memory]]
2. [[Java - Memory garbage collector]]