Tags: [[__Data_Engineering]]
#DataEngineering 

# Introduction
An immutable raw layer is a collection of data where we only append new records and we don't modify or delete any.
# Benefits
## 1. Debugging
If something breaks:
> “What did we actually receive?”

We can always go back and check.
## 2. Reprocessing
If logic in our data processing changes, we can use for it exactly the same date as we used previously.
## 3. Reproducibility
We can always reproduce previous results of data transformations by using the same raw data.
## 4. Auditability
We have a full history of:
- what arrived
- when it arrived