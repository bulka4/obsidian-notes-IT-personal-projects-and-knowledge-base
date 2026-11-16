Tags: [[_Java]] [[__Programming_languages]]
#Java #ProgrammingLanguages 

# Introduction
Stream is a variable type that makes it easier to iterate over lists / arrays and perform operations on them.

We convert a list / array into a stream like this:
```java
List<Integer> numbers = List.of(1, 2, 3, 4, 5);

Stream<Integer> stream = numbers.stream()
```

and we can perform on it operations:
```java
List<Integer> result = stream
    .filter(n -> n > 2)
    .map(n -> n * 10)
    .toList();

System.out.println(result); // [30, 40, 50]
```
