Tags: [[_DeepSpeed]], [[__Machine_Learning_Engineering]]

# Introduction
When DeepSpeed uses multiple GPUs for calculations, then each GPU performs calculations on a different set of numbers and results from each GPU need to be combined together to produce the final result.

So GPUs communicate with each other to exchange numbers needed for further calculations. NCCL ([[DeepSpeed - NCCL|link]]) is used for this communication.

#MachineLearning #MLEngineering 