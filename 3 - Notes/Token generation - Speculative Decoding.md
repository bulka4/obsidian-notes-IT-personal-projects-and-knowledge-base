Tags: [[__Machine_Learning]]

# Introduction
Speculative Decoding is a technique used when generating tokens ([[Token generation|link]]), to speed up generation.

It uses two models:
- Small model - Prepares a draft of an output sequence
- Big model - Verifies and corrects the draft prepared by the small model

It works like that:
- Small model generates $T$ tokens $t_1, \ldots, t_T$ 
- Big model verifies every token one by one:
	- If that token is probable according to the big model, then accept it
	- Otherwise, reject it
- If some token $t_k$ is rejected by the big model, we discard it and all the further tokens $t_{k+1}, \ldots, t_T$
- Regenerate the discarded tokens using the big model (create new tokens)

This allows the large model to “skip ahead” multiple tokens at once. It is faster because the big model performs fewer steps.

#MachineLearning 