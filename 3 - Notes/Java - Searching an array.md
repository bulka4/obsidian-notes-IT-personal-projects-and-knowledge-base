Tags: [[_Java]] [[__Programming_languages]]
#Java #ProgrammingLanguages 

# Find an index of an element
## For loop
Use a for loop:
```java
int[] numbers = {10, 20, 30, 40, 50};

int target = 30;

for (int i = 0; i < numbers.length; i++) {
    if (numbers[i] == target) {
        System.out.println("Found at index: " + i);
        break;
    }
}
```
## `Arrays.binarySearch()`
Use `Arrays.binarySearch()` (it requires the array to be sorted):
```java
import java.util.Arrays;

int[] numbers = {10, 20, 30, 40, 50};

int index = Arrays.binarySearch(numbers, 30);

System.out.println(index); // 2
```
## `ArrayList.indexOf()`
```java
ArrayList<Integer> numbers = new ArrayList<>();

numbers.add(10);
numbers.add(20);
numbers.add(30);

int index = numbers.indexOf(20);

System.out.println(index); // 1
```
# Check whether an element exists
## `Arrays.asList().contains()` for String arrays
For object arrays (reference type), we can use:
```java
import java.util.Arrays;

String[] names = {"John", "Alice", "Bob"};

boolean exists = Arrays.asList(names).contains("Alice");

System.out.println(exists); // true
```

This only checks whether an element exists.
## `ArrayList.contains()`
`ArrayList.contains()` works for any element type:
```java
ArrayList<Integer> numbers = new ArrayList<>();
numbers.add(10);
numbers.add(20);

numbers.contains(10); // true
```