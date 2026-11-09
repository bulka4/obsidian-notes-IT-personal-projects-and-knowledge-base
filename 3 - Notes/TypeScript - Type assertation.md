Tags: [[_TypeScript]] [[__Programming_languages]]
#TypeScript #ProgrammingLanguages 

# Introduction
Type assertion allows us to explicitly tell TypeScript (and developer) of what type a given variable should be. TypeScript checks whether a variable is of that type during build (code compilation).

The syntax is:
```typescript
value as Type
```

For example:
```typescript
interface Task {
    id: number;
    status: "todo" | "in-progress" | "done";
}

const status = event.target.value as Task["status"];
```

