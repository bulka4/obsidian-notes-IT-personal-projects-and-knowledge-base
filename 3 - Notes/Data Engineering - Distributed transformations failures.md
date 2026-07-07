Tags: [[__Data_Engineering]]
#DataEngineering 

# Introduction
When during a distributed transformations consisting of many tasks (e.g. in Spark), only some of those tasks fail, that's a problem. In that case, there are a few options:
- Restart an entire process
- Restart only failed tasks

To restart only failed tasks we need checkpointing which saves information about the progress of calculations.