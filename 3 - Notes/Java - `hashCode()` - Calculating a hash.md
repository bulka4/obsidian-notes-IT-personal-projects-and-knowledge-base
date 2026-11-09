Tags: [[_Java]] [[__Programming_languages]]
#Java #ProgrammingLanguages 

# Introduction
Every Java object has a `hashCode()` method.

By default, `Object.hashCode()` provides a hash based on object identity. You can override it to calculate a hash based on the object's contents.

For example:
```java
class User {
    int id;

    User(int id) {
        this.id = id;
    }

	@Override
	public int hashCode() {
	    return Integer.hashCode(id);
	}
}
```

Now two users with the same `id` will have the same hash code.