Tags: [[_Java]] [[__Programming_languages]]
#Java #ProgrammingLanguages 

# Introduction
An enum represents a predefined set of possible values:
```java
public enum TaskStatus {
    todo,
    in_progress,
    done
}
```

You can then use it as a variable type:
```java
TaskStatus status = TaskStatus.TODO;

status = TaskStatus.DONE;
```

You cannot assign arbitrary values:
```java
TaskStatus status = "DONE"; // Compile-time error
```

This provides type safety: the variable can only contain one of the defined enum values.
# Using enums with switch
Enums work very well with `switch` statements:
```java
TaskStatus status = TaskStatus.IN_PROGRESS;

switch (status) {
    case TODO:
        System.out.println("Task hasn't started");
        break;

    case IN_PROGRESS:
        System.out.println("Task is being worked on");
        break;

    case DONE:
        System.out.println("Task is completed");
        break;
}
```

You can also use the newer switch expression syntax:
```java
String description = switch (status) {
    case TODO -> "Not started";
    case IN_PROGRESS -> "In progress";
    case DONE -> "Completed";
};
```
# Enums can have fields, constructors and methods
Enums are more powerful than just named constants. They can contain data and behaviour.
```java
public enum TaskStatus {
	// values with descriptions
    TODO("Waiting to start"),
    IN_PROGRESS("Currently being worked on"),
    DONE("Completed");

	// this.description corresponds to the value description ("Waiting to start"
	// , "Completed", etc.)
    private final String description;

    TaskStatus(String description) {
        this.description = description;
    }

    public String getDescription() {
        return description;
    }
}
```

Usage:
```java
TaskStatus status = TaskStatus.DONE;

System.out.println(status.getDescription()); // prints Completed
```

Notice:
- Each enum constant is an instance of the enum type.    
- The constructor is called for each constant.    
- Enum constructors cannot be public or protected.    
- Enum constants are implicitly `public static final`.
# Useful built-in enum methods
Java provides several useful methods:
```java
// Returns all enum constants
TaskStatus[] statuses = TaskStatus.values();

// Returns the enum constant by name
TaskStatus status = TaskStatus.valueOf("DONE");

// Returns the name
String name = status.name();

// Returns its position (starting from 0)
int position = status.ordinal();
```

Be careful with `ordinal()`: it's generally not a good idea to use enum positions as persistent identifiers because changing the declaration order changes those numbers.
# Enums vs Strings
Why not simply use strings?
```java
String status = "DONE";
```

Because strings allow arbitrary values:
```java
status = "COMPLETED"; // No compile-time error
status = "DON";       // Typo, also no compile-time error
```

With enums:
```java
TaskStatus status = TaskStatus.DONE;
```

You get:
- Compile-time type safety.    
- A predefined set of allowed values.    
- Easier use with `switch`.    
- The ability to associate behaviour and data with each value.