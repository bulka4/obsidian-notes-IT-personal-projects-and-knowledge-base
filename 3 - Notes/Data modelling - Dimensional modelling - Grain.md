Tags: [[__Data_Engineering]] [[_Data_modelling]]
#DataEngineering #DataModelling 

# Introduction
Grain is the level of detail in a fact table.

It defines:
> “What does one row in the fact table represent?”
## Examples of grain:
- One row per order
- One row per order line item
- One row per daily product sales
- One row per user click event
## Why it matters
If grain is wrong:
- metrics become inconsistent
- joins break logic
- aggregation errors happen

👉 In practice, most dimensional modeling failures come from unclear grain.