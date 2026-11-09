Tags: [[_TypeScript]] [[__Programming_languages]]
#TypeScript #ProgrammingLanguages 

# Introduction
Interfaces allow us to define the expected structure of an object. They describe what properties and methods an object must have and what types those properties should use:
```typescript
interface User {
    id: number;
    name: string;
    greet: (message: string) => string;
}

const user: User = {
    id: 1,
    name: "John",

    greet: (message) => {return message};
};

user.greet("Hello!");
```

Function property in the interface definition `greet: (message: string) => string;` just specifies what arguments are available and what this function returns.