Tags: [[__Data_Engineering]] [[_Data_modelling]]
#DataEngineering #DataModelling 

# Introduction
A factless fact table is a fact table with:
- no numeric measures
- only foreign keys
## Use case
Tracking events like:
- attendance
- enrollment
- participation

Example:  
`| StudentID | ClassID | DateID |`

Meaning: “student attended class”