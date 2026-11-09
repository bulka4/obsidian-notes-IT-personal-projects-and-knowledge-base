Tags: [[_Java]] [[__Programming_languages]]
#Java #ProgrammingLanguages 

# Introduction
An `ArrayList` is a dynamically resizable collection. It stores objects (references), not primitives ([[Java - Data types - Primitive and Reference variables|link]]).

`Array` - Fixed size:
```java
int[] numbers = new int[3];

numbers[0] = 10;
numbers[1] = 20;
numbers[2] = 30;
```

`ArrayList` - dynamic size:
```java
ArrayList<Integer> numbers = new ArrayList<>();

numbers.add(10);
numbers.add(20);
numbers.add(30);
```

An `ArrayList` can grow or shrink as you add or remove elements.

An `ArrayList` can store either only one type or different ones:
```java
// can store only integers
ArrayList<Integer> numbers = new ArrayList<>();
numbers.add('a') // gives compile-time error

// can store different types
List names = new ArrayList();
numbers.add('a') // works
numbers.add(1) // works
```

When retrieving an element from an `ArrayList`, we need casting to ensure what is the returned type:
```java
List names = new ArrayList();
numbers.add('a') // works
numbers.add(1) // works

String name = (String) names.get(0);
```
