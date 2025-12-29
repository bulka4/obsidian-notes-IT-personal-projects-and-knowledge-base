Tags: [[_DeepSpeed]], [[__Machine_Learning_Engineering]]

# Introduction
This document describes how to deal with a situation when we get a NaN or Inf values because of a finite-precision numeric formats used ([[Numeric formats (precision) - Calculation errors|link]]) during training models ([[Training machine learning models - Introduction|link]]) and operations like all-reduce ([[Collective operations|link]]).
# Gradient synchronization checks
When gradients calculated by different GPUs are all-reduced and a single GPUs produces a NaN or Inf because of a numeric format used, then we will get those values also in the output of all-reduce (if one element is NaN or Inf then the entire sum / max / average is also NaN or Inf).

'Gradient synchronization checks' means that we check if gradients calculated by each GPU contain Infs or Nans and those values are skipped (we don't update model weights at all for a given data batch ([[Batching|link]]), for which we got those values)
# Reduce-scatter instead of all-reduce
Instead of using all-reduce ([[Collective operations|link]]), it is preferred to use reduce-scatter and then all-gather to reconstruct the full tensor if needed.

Thanks to that:
- There is less data being sent to each GPU so it improves a bandwidth
- There is less accumulation error (like described here - [[DeepSpeed - Numerical stability|link]])
	- That's because each GPU reduces only a part of the tensor so fewer values are summed per reduction
- Less NaN propagation risk
	- We can detect whether results on one GPU contains NaNs and skip those results like explained in the previous section 'Gradient synchronization checks'

#DeepSpeed #MLEngineering 