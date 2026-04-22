Tags: [[__Data_Engineering]]
#DataEngineering 

# Introduction
An upsert / "merge into" operation is an operation where we insert rows from a source table into a target one such that:
- If a row from the source doesn't exist in the target -> insert it into the target
- If a row from the source already exists in the target -> update it in the target
- If a row from the target doesn't exists in the source -> delete it from the target