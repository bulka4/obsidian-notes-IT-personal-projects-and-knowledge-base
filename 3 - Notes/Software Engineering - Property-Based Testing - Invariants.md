Tags: [[_Software_Engineering]]
#SoftwareEngineering 

# Introduction
An invariant is a condition that should always remain true during the execution of a system or operation. It is used in Property-Based Testing ([[Software Engineering - Property-Based Testing|link]]).

Examples:
- **Bank account:** balance should never be negative (if overdraft is not allowed).
- **Database transaction:** after a transaction commits, data must satisfy all constraints.
- **Queue:** the number of items cannot be negative.
- **Sorting algorithm:** the output must always contain the same elements as the input.
- **Distributed system:** committed data should not disappear after a node failure.