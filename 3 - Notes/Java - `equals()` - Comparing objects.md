Tags: [[_Java]] [[__Programming_languages]]
#Java #ProgrammingLanguages 

# Introduction
By default, Java's `Object.equals()` compares object references (whether they are the same object), not whether their contents are equal.

For example:
```java
class User {
    int id;

    User(int id) {
        this.id = id;
    }
}

User user1 = new User(1);
User user2 = new User(1);

System.out.println(user1.equals(user2)); // false
```

Although both objects have the same `id`, they are different objects in memory.

You can override `equals()` to define what makes two objects logically equal:
```java
class User {
    int id;

    User(int id) {
        this.id = id;
    }

    @Override
    public boolean equals(Object obj) {
        if (this == obj) return true;

        if (!(obj instanceof User other)) {
            return false;
        }

        return this.id == other.id;
    }
}
```

Now:
```java
User user1 = new User(1);
User user2 = new User(1);

System.out.println(user1.equals(user2)); // true
```