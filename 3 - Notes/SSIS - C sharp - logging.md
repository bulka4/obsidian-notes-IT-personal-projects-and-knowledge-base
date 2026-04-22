Tags: [[_Visual_Studio_solutions]]
#VisualStudioSolutions 

# Introduction
To write logs in a C# script which is executed in SSIS and see them in SSIS output (terminal), we need to use this function:
```c#
bool fireAgainNew = true; 
ComponentMetaData.FireInformation(0, "ExcelHandler", msg, "", 0, ref fireAgainNew);
```

But this works only in the `ScriptMain` class. If we create an object of another class inside the `ScriptMain` class:
```c#
public class ScriptMain : UserComponent
{
	AnotherClass object = new AnotherClass(...)
}
```

and we want to write logs from a function from another class `AnotherClass`, we need to do it like this:
```c#
public class ScriptMain : UserComponent
{
	AnotherClass object = new AnotherClass(
		// Pass a function for writting logs as a parameter
		msg => { bool fireAgainNew = true; ComponentMetaData.FireInformation(0, "ExcelHandler", msg, "", 0, ref fireAgainNew);
	)
}

public class AnotherClass
{
	// _log attribute will be a function for writting logs
	private Action<string> _log;
	
	private AnotherClass(Action<string> log)
	{
		// The log parameter is a function for writting logs. Assign it to the 
		// _log attribute
		_log = log
	}
	
	private void WriteLogs(string message)
	{
		// write a message which will be visible in logs
		_log(message)
	}
}
```
