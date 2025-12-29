Tags: [[_DeepSpeed]], [[__Machine_Learning_Engineering]]

# Introduction
MQA (Multi-Query Attention) ([[DeepSpeed - MQA and GQA|link]]) and GQA (Grouped-Query attention) ([[Neural Network - Grouped-Query Attention (GQA) layer|link]]) can be used when training a transformer model to further reduce computational cost by reducing number of K and V vectors we keep saved in cache ([[DeepSpeed - KV caching|link]]).

Normally, in a multi-head attention (MHA) ([[Neural Network - Multi-Head Attention (MHA) layer|link]]) we have separate matrices $Q_h, K_h, V_h$ per each head $h$. 
- MQA has separate Query matrices $Q_h$ per head and only one pair of Key-Value matrices $K, V$ 
- GQA has separate Query matrices $Q_h$ per head and multiple pairs of Key-Value matrices $\large K_i, V_i$, one per group of Query matrices $\Large Q_{I_i} = \{Q_j : j \in I_i\}$ 

#DeepSpeed #MLEngineering 