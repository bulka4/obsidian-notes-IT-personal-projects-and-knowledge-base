Tags: [[_Java]] [[__Programming_languages]]
#Java #ProgrammingLanguages 

# try and catch
```java
try {
    int[] numbers = {1, 2, 3};
    System.out.println(numbers[5]);
} catch (ArithmeticException e) {
    System.out.println("Arithmetic error");
} catch (ArrayIndexOutOfBoundsException e) {
    System.out.println("Invalid array index");
} catch (Exception e) {
    System.out.println("Some other error occurred");
}
```
# Finally
The `finally` block executes whether an exception occurs or not:
```java
try {
    int result = 10 / 2;
} catch (ArithmeticException e) {
    System.out.println("Error");
} finally {
    System.out.println("Execution finished");
}
```
# Throw
You can explicitly throw an exception yourself using `throw`.
```java
public void setAge(int age) {
    if (age < 0) {
        throw new IllegalArgumentException("Age cannot be negative");
    }
}
```
# throws
`throws` declares that a method can propagate certain exceptions to the code that calls it.
```java
public void readFile() throws IOException {
    // Code that reads a file
}
```

It informs the caller that they must then either handle the exception with `try-catch` or declare it with `throws` as well (for checked exceptions).
# Related topics
1. [[Java - Exception classes]]
2. [[Java - Checked and unchecked exceptions]]
	1. [[Java - How the compiler check exceptions]]