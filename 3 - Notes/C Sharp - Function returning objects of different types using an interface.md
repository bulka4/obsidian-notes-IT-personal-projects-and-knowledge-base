Tags: [[__Programming_languages]] [[_C_sharp]]
#ProgrammingLanguages #CSharp 

# Introduction
When we have a function which can return objects of different types, we can use an interface ([[C Sharp - Interface|link]]).

We define an interface and classes which implements it:
```c#
public interface IResult
{
    bool IsSuccess { get; }
}

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

And we can use it in a function as a type of the returned object in the function's definition:
```c#
public IResult GetResult(bool ok)
{
    if (ok)
        return new SuccessResult { Data = "All good" };
    else
        return new ErrorResult { ErrorMessage = "Something failed" };
}
```

Function's result can be used like that:
```c#
var result = GetResult(true);

if (result.IsSuccess)
{
	// Create an object of the SuccessResult class
    var success = (SuccessResult)result;
    Console.WriteLine(success.Data);
}
else
{
	// Create an object of the ErrorResult class
    var error = (ErrorResult)result;
    Console.WriteLine(error.ErrorMessage);
}
```
