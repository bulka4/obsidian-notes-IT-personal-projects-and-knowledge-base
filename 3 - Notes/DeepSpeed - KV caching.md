Tags: [[_DeepSpeed]], [[__Machine_Learning_Engineering]]

# Introduction
KV caching is used when a transformer model ([[Transformer model|link]]) generates tokens ([[Token generation|link]]), like generating an answer for a question.

For generating each token, model needs to calculate vectors K and V (Key and Value) per each token generated so far.

To avoid recalculating those vectors all the time, they are cached (saved) for later use.
# Blockwise KV Storage (Paged KV-cache)
More information about blockwise KV Storage (Paged KV-cache) can be found here - [[DeepSpeed - Blockwise KV Storage (Paged KV-cache)|link]].
# Rolling KV caching
More information about rolling KV caching can be found here - [[DeepSpeed - Blockwise KV Storage (Paged KV-cache)|link]].

#DeepSpeed #MLEngineering 