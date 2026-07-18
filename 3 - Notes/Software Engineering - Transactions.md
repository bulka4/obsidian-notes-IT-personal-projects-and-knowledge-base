Tags: [[_Software_Engineering]]
#SoftwareEngineering 

# Introduction
A transaction means a group of operations that is treated as one logical unit of work: it either completes fully or does not happen at all.
# Example
For example, moving 100 USD consists of two operations:
1. Remove 100 USD from account A
2. Add 100 USD to account B

Without a transaction, a failure could happen between those two operations:
1. Removing 100 USD - successful
2. Adding 100 USD - failed

So we end up with money disappeared.

With a transaction, we make sure that when money are removed from one account then they are added to another account or we don't remove money at all.
# Related concepts
- ACID transactions ([[Software Engineering - ACID transactions|link]]) - One common model of transactions are ACID transactions
- Rollback ([[Software Engineering - Rollback|link]]) - Undo changes done by a transaciton