Tags: [[__Programming_languages]] [[_C_sharp]]
#ProgrammingLanguages #CSharp 

# Constructing a class
Defining attributed and functions:
```c#
internal class ClassName
{
    public string Attr { get; set; }

    private static async void FuncAsync(...)
    {
        // method body
    }
}
```
`get` and `set` keywords next to the attribute can be used for controlling how we can assign a value to it and read it. If we leave them like in this example, then there is no control (everything allowed).
# Constructor
Constructor is a function called automatically when creating an object of a class. It is a function with the same name as the class:
```c#
internal class ClassName
{
    public string Attr { get; set; }

	// Constructor
    public ClassName(...)
    {
        // method body
    }
}
```
# Create an object
Create an object and call a constructor:
```c#
ClassName object = new ClassName(arg1)
```

Create an object without calling a constructor:
```c#
ClassName object = new ClassName{arg1}
```