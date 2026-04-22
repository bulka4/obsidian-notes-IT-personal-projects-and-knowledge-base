Tags: [[__Data_Engineering]] [[_Data_modelling]]
#DataEngineering #DataModelling 

# Introduction
This is a **very important real-world concept**
## Problem it solves
What happens when dimension data changes over time?

Example:
- customer changes city
- product changes category
## Types:
### Type 1
- overwrite old value (no history)
### Type 2 ⭐ (most important)
- keep history by creating new rows
- adds validity dates or versioning
### Type 3
- keeps limited history (previous value columns)