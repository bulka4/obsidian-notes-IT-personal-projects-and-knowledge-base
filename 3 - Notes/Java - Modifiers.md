Tags: [[_Java]] [[__Programming_languages]]
#Java #ProgrammingLanguages 

# Access modifiers
Access modifiers determine where a class, field (attribute), method or constructor can be accessed from.

Java has four access levels:

| Modifier    | Accessibility                                                             |
| ----------- | ------------------------------------------------------------------------- |
| `public`    | Accessible from anywhere (subject to module visibility).                  |
| `protected` | Accessible within the same package and from subclasses in other packages. |
| `private`   | Accessible only within the declaring class.                               |
| No modifier | Package-private: accessible only within the same package.                 |

Which access modifiers are available for different objects:

| Declaration | Access modifiers              |
| ----------- | ----------------------------- |
| Class       | `public` (or package-private) |
| Field       | All four access levels        |
| Method      | All four access levels        |
| Constructor | All four access levels        |
## Benefits
[[Java - Access modifiers - Benefits]]
# Non-access modifiers
[[Java - Non-access modifiers]]
# Modifiers can be combined
You can combine access and non-access modifiers:
```java
public static final int MAX_USERS = 100;
```

Here:
- `public` = access modifier.
- `static` = non-access modifier.
- `final` = non-access modifier.
- `int` = type.
- `MAX_USERS` = field name.
# Access modifiers and inheritance
How access modifiers matter for class inheritance ([[Java - Class inheritance (extending a class)|link]]):

|Modifier|Accessible in child class?|
|---|---|
|`public`|Yes|
|`protected`|Yes|
|package-private (no modifier)|Yes, if in the same package|
|`private`|No, not directly|
