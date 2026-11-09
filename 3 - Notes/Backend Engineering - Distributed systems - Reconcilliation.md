Tags: [[__Backend_Engineering]]
#BackendEngineering 

# Introduction
Reconciliation is a process of comparing two or more representations of data to identify discrepancies and taking actions to make them consistent with each other or with an expected state.

It is particularly useful in distributed systems, financial systems, and applications that integrate multiple services.
# 1. Why do we need reconciliation?
In a backend system, the same logical information can exist in multiple places.

For example, consider an e-commerce application:
- Your application has a database containing orders.    
- A payment provider has its own database containing payment transactions.    
- A warehouse system tracks inventory and fulfillment.    

These systems communicate over networks, and operations can fail at different stages.

For example:
1. Your application sends a payment request.    
2. The payment provider successfully charges the customer.    
3. The response gets lost because of a network failure.    
4. Your application never receives confirmation and still considers the payment pending.    

Now the two systems disagree:

|System|Payment status|
|---|---|
|Your application|Pending|
|Payment provider|Completed|

This is an inconsistency.

Reconciliation allows your application to discover and correct it, even though the original operation failed from your application's perspective.
# 2. How does reconciliation work?
A typical reconciliation process consists of several stages.

1. Collect data    
    Retrieve relevant information from the systems being compared.    
    
    For example, retrieve all pending payments from your database and their statuses from the payment provider.    
2. Match records    
    Determine which records in different systems represent the same logical entity.
    
    For example, match payments using a transaction ID or external payment reference.    
1. Compare states    
    Identify discrepancies between the records.
    
    For example, your database says `pending`, while the provider says `completed`.    
1. Determine corrective actions    
    Decide what should happen based on the discrepancy.
    
    For example, update your internal payment status to `completed`.    
1. Apply corrections    
    Execute the necessary operations, potentially involving multiple systems.    
2. Verify consistency    
    Check whether the discrepancies have been resolved. Unresolved cases can be retried or escalated for manual investigation.    
# 3. What kinds of inconsistencies can reconciliation detect?
Some examples:

|Situation|Possible corrective action|
|---|---|
|Payment provider completed payment, but your DB says pending|Update payment status|
|Your DB says payment completed, but provider says failed|Investigate and potentially refund|
|Payment exists in provider but not in your DB|Create missing record or investigate|
|Inventory differs between warehouse and application|Synchronize inventory|
|Two systems have different customer information|Apply the authoritative value or merge|
|A message was processed twice|Detect duplicate and correct the resulting state|

Notice that not all discrepancies are conflicts. Sometimes a record is simply missing, an operation was interrupted, or one system failed to receive an update.