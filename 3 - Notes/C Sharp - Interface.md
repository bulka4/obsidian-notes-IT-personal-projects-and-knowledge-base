Tags: [[__Programming_languages]] [[_C_sharp]]
#ProgrammingLanguages #CSharp 

# Introduction
We define an interface this way:
```c#
public interface IResult
{
    bool IsSuccess { get; }
}
```

It has properties and methods (like attributes and functions in a class).

It can be implemented in classes:
```c#
public class SuccessResult : IResult
{
    public bool IsSuccess => true;
    public string Data { get; set; }
}

public class ErrorResult : IResult
{
    public bool IsSuccess => false;
    public string ErrorMessage { get; set; }
}
```

Every class that implements an interface, needs to provide values for all the properties of the interface.
# A variable of an interface type
We create a variable of an interface type by creating an object of one of the classes which implements that interface:
```c#
IResult result = new SuccessResult();
```
or:
```c#
IResult result = new ErrorResult();
```

A variable of an interface type always points to a specific object of one of the classes which implements that interface.

We can access interface properties but we can't access other attributes of the class which is behind this interface:
```c#
IResult result = new SuccessResult();
result.isSuccess // <- works
result.Data // <- not possible
```

`result` doesn't hold any data, it only points to an object of the `SuccessResult` class and when we access its property like `result.isSuccess`, then we are getting not a value of an interface property but value of the object of the class which it points to.

To access other attributes of the class which is behind an interface, we need to convert it into that class first:
```c#
var success = (SuccessResult)result;
Console.WriteLine(success.Data); // <-works
```
# Checking what is the class of an object which a variable of an interface type points to
```c#
IResult result = new SuccessResult();
Console.WriteLine(result.GetType().Name);  // prints "SuccessResult"
```
# Properties
## Interface can't be instantiated
We can't instantiate an interface like a class:
```c#
IResult r = new IResult(); // ❌ impossible
```
# Applications
Interface can be used:
- When defining a function which can return objects of different types ([[C Sharp - Function returning objects of different types using an interface]])