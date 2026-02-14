Tags: [[__Programming_languages]] [[_C_sharp]]
#ProgrammingLanguages #CSharp 

# Public
Public function is accessible from anywhere:
```c#
public void func(){}
```
# Private
Private function is accessible only inside the same class
```c#
private void func(){}
```
# Protected
Protected function is accessible inside the same class and subclasses
```c#
protected void func(){}
```
# Static
Static function belongs to the class, not an object. We don't need to create an instance of a class to use it.
```c#
public static void func(){}
```