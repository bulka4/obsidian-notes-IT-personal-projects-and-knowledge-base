Tags: [[_Java]] [[__Programming_languages]]
#Java #ProgrammingLanguages 

# Introduction
If two objects are equal according to `equals()`, they MUST have the same `hashCode()`.

However, the reverse is not required: two objects can have the same hash code but not be equal.

For example:

|Object|`equals()`|`hashCode()`|
|---|---|---|
|User(1) and User(1)|true|Same|
|User(1) and User(2)|false|May be same or different|
