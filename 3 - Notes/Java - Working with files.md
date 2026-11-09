Tags: [[_Java]] [[__Programming_languages]]
#Java #ProgrammingLanguages 

# Introduction
In Java, you can read and write files using several APIs. The most commonly used modern approach is `java.nio.file`, particularly the `Path` and `Files` classes.
# Working with file paths
First, you need to represent a file location.

Java provides the `Path` interface and the `Paths` utility class.
```java
import java.nio.file.Path;
import java.nio.file.Paths;

Path path = Paths.get("data.txt");
```

You can also specify an absolute path:
```java
Path path = Paths.get("C:/Users/John/Documents/data.txt");
```

A `Path` object represents a file system location. It doesn't necessarily mean that the file exists.
# Writing to files
The simplest way to write text to a file is `Files.writeString()`.
```java
import java.nio.file.Files;
import java.nio.file.Path;
import java.io.IOException;

public class Main {
    public static void main(String[] args) {
        Path path = Path.of("data.txt");

        try {
            Files.writeString(path, "Hello, world!");
        } catch (IOException e) {
            System.out.println("Error writing file: " + e.getMessage());
        }
    }
}
```

A few important details:
- If the file doesn't exist, Java creates it.    
- If the file already exists, its contents are overwritten by default.    
- `IOException` is a checked exception, so you must handle it or declare it.    

Appending instead of overwriting

You can use `StandardOpenOption.APPEND`:
```java
Files.writeString(
    path,
    "\nAnother line",
    StandardOpenOption.CREATE,
    StandardOpenOption.APPEND
);
```

Here:
- `CREATE` creates the file if it doesn't exist.    
- `APPEND` adds content to the end instead of overwriting it.    
# 3. Reading files
To read an entire text file into a `String`:
```java
String content = Files.readString(path);

System.out.println(content);
```

For example:
```java
Path path = Path.of("data.txt");

try {
    String content = Files.readString(path);
    System.out.println(content);
} catch (IOException e) {
    System.out.println("Error reading file: " + e.getMessage());
}
```

You can also read a file line by line:
```java
List<String> lines = Files.readAllLines(path);

for (String line : lines) {
    System.out.println(line);
}
```

This is useful when working with CSV files, configuration files, logs, etc. Note that `readAllLines()` loads all lines into memory.
# 4. Reading large files line by line
If the file is large, you might not want to load the entire file into memory.

You can use `BufferedReader`:
```java
try (BufferedReader reader = Files.newBufferedReader(path)) {
    String line;

    while ((line = reader.readLine()) != null) {
        System.out.println(line);
    }
} catch (IOException e) {
    System.out.println(e.getMessage());
}
```

`BufferedReader` reads the file incrementally.

Notice the `try (...)` syntax. This is called try-with-resources.

It automatically closes the reader when the block finishes, even if an exception occurs.
# 5. Writing large files incrementally
Similarly, you can use `BufferedWriter`:
```java
try (BufferedWriter writer = Files.newBufferedWriter(path)) {
    writer.write("First line");
    writer.newLine();
    writer.write("Second line");
} catch (IOException e) {
    System.out.println(e.getMessage());
}
```

This is useful when you want to generate files incrementally rather than constructing one enormous string in memory.
# 6. Other useful file operations
The `Files` class provides many utility methods.
```java
Path path = Path.of("data.txt");

// Check whether a file exists
boolean exists = Files.exists(path);

// Delete a file
Files.delete(path);

// Delete only if it exists
Files.deleteIfExists(path);

// Copy a file
Files.copy(path, Path.of("backup.txt"));

// Move or rename a file
Files.move(path, Path.of("renamed.txt"));

// Get file size in bytes
long size = Files.size(path);
```

You can also create directories:
```java
Files.createDirectory(Path.of("myFolder"));
```

Or create a directory and any missing parent directories:
```java
Files.createDirectories(Path.of("parent/child/folder"));
```
