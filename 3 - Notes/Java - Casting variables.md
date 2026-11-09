Tags: [[_Java]] [[__Programming_languages]]
#Java #ProgrammingLanguages 

# Introduction
Casting means explicitly telling Java to treat a value as a particular type.

For example:
```java
Object value = "Hello";

String text = (String) value;
```

Here's what happens:
1. `value` is declared as `Object`, so Java only knows its declared type is `Object`.    
2. The actual object stored in it is a `String`.    
3. `(String)` tells Java to treat it as a `String`.    
4. Java checks at runtime whether the actual object is compatible with `String`.    

If it isn't, Java throws a `ClassCastException`.
```java
Object value = 123;

String text = (String) value; // ClassCastException
```

Important distinction:
- Casting does not change the actual object's type.    
- It changes how Java treats the reference, allowing access to members of the target type.    

There are also implicit conversions, such as:
```java
int number = 10;
double decimal = number; // Automatic conversion
```

This is called widening primitive conversion, rather than reference casting.