Tags: [[__Machine_Learning_Engineering]], [[_Ray]]
#MLEngineering #Ray 

# Introduction
- Python worker processes that actually run your task/actor code.
- They’re started on-demand by the Raylet (not all run all the time).
- Can be many per node, depending on task concurrency.