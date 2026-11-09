Tags: [[_Java]] [[__Programming_languages]]
#Java #ProgrammingLanguages 

# Introduction
Exception classes that represent different categories of problems:
# Throwable
`Throwable` is the root class of everything that can be thrown using `throw` and caught using `catch`.

It has two main subclasses:
- `Error`
- `Exception`
# Error
`Error` represents serious problems, usually related to the JVM or system resources.

Examples:
- `OutOfMemoryError` – JVM cannot allocate more memory.
- `StackOverflowError` – the call stack has run out of space.

You generally don't try to handle these in normal application code because they often indicate serious problems that your application cannot recover from.
# 3. Exception
`Exception` represents conditions that an application might want to handle.

Examples:
- `IOException` – an input/output operation failed.
- `SQLException` – a database operation failed
- `FileNotFoundException` – a file couldn't be found.

Exceptions can be either checked or unchecked.
# 4. RuntimeException
`RuntimeException` is a subclass of `Exception`.

It represents unchecked exceptions, which the compiler doesn't require you to catch or declare using `throws`.

Examples:
- `NullPointerException`
- `IllegalArgumentException`
- `IndexOutOfBoundsException`
- `NumberFormatException`