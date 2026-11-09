Tags: [[__Software_Engineering]]
#SoftwareEngineering 

# Introduction
Unexpected or inconsistent results caused by interactions between concurrent database transactions. Examples include dirty reads, non-repeatable reads and phantom reads.
# Examples
## Inconsistent reads
A request reads multiple pieces of related data while another transaction is modifying them.

Example: You have two accounts with a combined balance of €1,000. A transaction transfers €200 from one account to another.

Another request reads the first account before the transfer and the second account after the transfer.

It might observe a combination of values that never represented a consistent database state.

Solutions:
- Database transactions.
- Appropriate transaction isolation levels.
- Snapshot isolation or serializable isolation, depending on requirements.