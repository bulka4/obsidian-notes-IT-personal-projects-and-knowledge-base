Tags: [[__Machine_Learning]]

# Introduction
Multi-query attention (MQA) neural network layer is a simplified version of a multi-head attention (MHA) ([[Neural Network - Multi-Head Attention (MHA) layer|link]]).

In MHA, we have separate matrices $Q_h, K_h, V_h$ per each head $h$, while in MQA we have only separate Query matrices per head $Q_h$ , while matrices $K, V$ are the same for each head.

Thanks to this, we have much less computations to do but performance might be slightly worse.

#MachineLearning 