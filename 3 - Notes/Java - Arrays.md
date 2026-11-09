Tags: [[_Java]] [[__Programming_languages]]
#Java #ProgrammingLanguages 

# Declaring and initializing arrays
There are several ways to create an array.

Option 1: Declare and initialize together
```java
int[] numbers = {10, 20, 30, 40, 50};
```

Option 2: Specify the array size
```java
int[] numbers = new int[5];
```

This creates an array with five elements, initially set to `0`.

You can assign values afterward:
```java
numbers[0] = 10;
numbers[1] = 20;
numbers[2] = 30;
```

Option 3: Declare first, initialize later
```java
int[] numbers;

numbers = new int[]{10, 20, 30};
```

Notice that Java uses `new` to create the array object.

We need to define array size when creating it (and it can't be changed later, we need to use `ArrayList` to be able to change the size).
# Accessing array elements
Arrays use zero-based indexing, meaning the first element has index `0`.
```java
int[] numbers = {10, 20, 30, 40, 50};

System.out.println(numbers[0]); // 10
System.out.println(numbers[1]); // 20
System.out.println(numbers[4]); // 50
```

You can also modify elements:
```java
numbers[0] = 100;
```

Trying to access an invalid index results in an `ArrayIndexOutOfBoundsException`.
# 3. Array length
You can get the number of elements using the `.length` property:
```java
int[] numbers = {10, 20, 30};

System.out.println(numbers.length); // 3
```

Note that `length` is a property, not a method. You don't use parentheses.
# 4. Iterating over arrays
There are two common approaches.

Traditional for loop:
```java
int[] numbers = {10, 20, 30};

for (int i = 0; i < numbers.length; i++) {
    System.out.println(numbers[i]);
}
```

This is useful when you need the index.

Enhanced for loop (for-each):
```java
int[] numbers = {10, 20, 30};

for (int number : numbers) {
    System.out.println(number);
}
```

This iterates directly over the elements without requiring indexes.
# 5. Arrays of different types
Arrays can store primitive types:
```java
int[] numbers = {1, 2, 3};
double[] prices = {10.5, 20.5};
boolean[] flags = {true, false};
char[] letters = {'A', 'B', 'C'};
```

They can also store objects:
```java
String[] names = {"John", "Alice", "Bob"};

Task[] tasks = {
    new Task(),
    new Task(),
    new Task()
};
```

Remember: an array can only contain elements of one declared type. For example, a `String[]` cannot directly contain integers.
# 6. Multidimensional arrays
Java supports arrays containing other arrays.

For example, a two-dimensional array:
```java
int[][] matrix = {
    {1, 2, 3},
    {4, 5, 6},
    {7, 8, 9}
};
```

You can access individual elements using two indexes:
```java
System.out.println(matrix[0][0]); // 1
System.out.println(matrix[1][2]); // 6
System.out.println(matrix[2][1]); // 8
```

You can iterate over it using nested loops:
```java
for (int i = 0; i < matrix.length; i++) {
    for (int j = 0; j < matrix[i].length; j++) {
        System.out.println(matrix[i][j]);
    }
}
```

An important detail: Java multidimensional arrays are actually arrays containing other arrays. Their rows don't necessarily need to have the same length.
# 7. Important characteristics of Java arrays

|Characteristic|Description|
|---|---|
|Fixed size|Once created, the array size cannot change.|
|Same element type|All elements must match the declared type.|
|Zero-based indexing|First element has index `0`.|
|Objects|Arrays are objects in Java, including arrays of primitives.|
|Default values|Elements are automatically initialized.|

Default values:

|Type|Default value|
|---|---|
|`int`|`0`|
|`double`|`0.0`|
|`boolean`|`false`|
|`char`|`'\u0000'`|
|Object references (e.g. `String`)|`null`|
# 8. ArrayList
[[Java - ArrayList]]
# Searching an array
[[Java - Searching an array]]