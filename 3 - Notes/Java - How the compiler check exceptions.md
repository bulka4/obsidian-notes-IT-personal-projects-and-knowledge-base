Tags: [[_Java]] [[__Programming_languages]]
#Java #ProgrammingLanguages 

# Introduction
For checked exceptions ([[Java - Checked and unchecked exceptions|link]]), the compiler checks whether your method handles or declares exceptions that can propagate out of it.

For example, when we call another method that declares a checked exception:
```java
public void readFile() throws IOException {
    // Read file
}

public void processFile() {
    readFile(); // COMPILATION ERROR
}
```

the compiler knows that the exception can appear in the `processFile` method because the `readFile` declares that it can throw an exception and `processFile` uses this method.

So the `processFile` must either handle this exception:
```java
public void processFile() {
    try {
        readFile();
    } catch (IOException e) {
        System.out.println("Reading failed");
    }
}
```

or declare that this exception can be thrown:
```java
public void processFile() throws IOException {
    readFile();
}
```
# How the compiler knows that an exception can appear
## A. You call another method that declares a checked exception.
```java
public void readFile() throws IOException {
    // Read file
}

public void processFile() {
    readFile(); // COMPILATION ERROR
}
```
## B. You explicitly throw a checked exception yourself
```java
public void processFile() {
    throw new IOException(); // COMPILATION ERROR
}
```