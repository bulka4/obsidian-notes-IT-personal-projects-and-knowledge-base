Tags: [[__Data_Engineering]] [[_Data_modelling]]
#DataEngineering #DataModelling 

# Introduction
## Idea
Combine many small flags/attributes into one dimension. Instead of many tiny dimensions → one “junk dimension”.
## Example
Before (in fact table):
`| OrderID | Revenue | is_returned | is_gift | payment_type | promo_flag |`

After (junk dimension approach):
- Fact table:
	`| OrderID | Revenue | JunkDimID |`
- Junk dimension:
	`| JunkDimID | is_returned | is_gift | payment_type | promo_flag |`