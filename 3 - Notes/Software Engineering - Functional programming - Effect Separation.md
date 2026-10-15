Tags: [[__Software_Engineering]]
#SoftwareEngineering 

# Introduction
Effect separation means keeping the code separate for:
- Pure business logic → pure function ([[Software Engineering - Functional programming - Pure Functions|link]]), calculations, rules, transformations
- Side effects (external dependencies outside of a function scope [[Software Engineering - Functional programming - Side effects|link]]) → database, network, filesystem, external systems

So we create one pure function with a business logic and a separate function which has side effects instead of creating one function that combines both.