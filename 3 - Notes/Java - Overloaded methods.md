Tags: [[_Java]] [[__Programming_languages]]
#Java #ProgrammingLanguages 

# Introduction
Overloaded methods are methods that share the same name but have different parameters.

A method's name plus its parameters define a method signature which is unique.

For example, we can have:
```java
static double add (double a, double b){
	return a + b
}

static double add (double a, double b, double c){
	return a + b + c
}
```

but we can't define `static double add (double a, double b)` twice (the same method name and parameters.