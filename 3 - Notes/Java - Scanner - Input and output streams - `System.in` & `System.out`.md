Tags: [[_Java]] [[__Programming_languages]]
#Java #ProgrammingLanguages 

# Introduction
`System.out` and `System.in` represent output and input streams and we can set up from where to take the input stream (keyboard, file, etc.) and where to send the output (again keyboard, file, etc.).
# System.out – output
`System.out` sends output, usually to the terminal (standard output) or to a file:

Print output in a terminal:
```java
System.out.print("Hello");
```

Save output in a file:
```java
System.setOut(new PrintStream("output.txt"));
System.out.println("Hello!");
```
# System.in – input
We can read input in a several ways.

Using `Scanner`:
```java
Scanner scanner = new Scanner(System.in);

String name = scanner.nextLine();
int age = scanner.nextInt();
```

Reading one byte from the input stream:
```java
int character = System.in.read();
```

Using `BufferedReader`:
```java
BufferedReader reader = new BufferedReader(
    new InputStreamReader(System.in)
);

String input = reader.readLine();
```
## Redirecting input
We can also redirect input from a file:

After setting up this:
```java
System.setIn(new FileInputStream("input.txt"));
```

`Scanner` reading from `System.in` will read from this file:
```java
Scanner scanner = new Scanner(System.in); // reads from a file
```
