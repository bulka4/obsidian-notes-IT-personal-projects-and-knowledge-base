Tags: [[_Visual_Studio_solutions]]
#VisualStudioSolutions 

# Introduction
When we create a C# task in SSIS and define table output variables, in C# we get automatically generated classes `ScriptBuffer` and `OutputNameBuffer`. 

They are used in C# to define how those outputs will look like (we add rows to them).

There are provided functions like:
- `AddRow` - Add row to the output table

We can provide values for columns like this:
```c#
private readonly OutputNameBuffer _nameBuffer;
_nameBuffer.AddRow();
_nameBuffer.columnName = 'a'
```