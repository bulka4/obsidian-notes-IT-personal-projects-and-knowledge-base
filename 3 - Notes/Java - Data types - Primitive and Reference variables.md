Tags: [[_Java]] [[__Programming_languages]]
#Java #ProgrammingLanguages 

# Primitive type
Primitive is a simple value (like a number) stored directly in memory (usually in a location known as the "stack").

Java has 8 primitive types:

| Type      | What it stores   | Example             |
| --------- | ---------------- | ------------------- |
| `byte`    | Small integer    | `byte x = 10;`      |
| `short`   | Integer          | `short x = 100;`    |
| `int`     | Integer          | `int x = 1000;`     |
| `long`    | Large integer    | `long x = 100000L;` |
| `float`   | Decimal number   | `float x = 1.5f;`   |
| `double`  | Decimal number   | `double x = 1.5;`   |
| `boolean` | True/false       | `boolean x = true;` |
| `char`    | Single character | `char x = 'A';`     |
# Reference type
Reference variables holds a reference to an object that allows to locate this object in memory.

The object is typically allocated in the "heap" memory and the reference variable in the "stack" memory (method's stack frame) ([[Java - Heap and stack memory|link]]).

Reference types (objects):
- `String`
- `ArrayList`
- Custom classes such as `User` or `Task`
- Arrays
- Interfaces and other class types

So when we write:
```java
User user = new User();
```

then:
- `User` - class name
- `user` - reference variable
- `new User()` - creates a new object that the `user` variable refers to
# Copying values
For primitive variables:
```java
int a = 10;
int b = a;

b = 20;

System.out.println(a); // 10
System.out.println(b); // 20
```

When you assign `a` to `b`, the value is copied but variables are kept separate (they can store different values).

For reference variables:
```java
User user1 = new User();
user1.name = "John";

User user2 = user1;

user2.name = "Alice";

System.out.println(user1.name); // Alice
```

This happens because `user1` and `user2` now reference the same object.
# Wrapper classes
[[Java - Wrapper classes]]
# Array data types
- `int[]` - Array with integers