Tags: [[__Machine_Learning]]

# Introduction
Transformer model is primarily used for token generation ([[Token generation|link]]), like generating answers for questions. 

It uses different neural network layers ([[Neural Network|link]]) mainly attention ([[Neural Network - Attention layer|link]]).

It consists of:
- Encoder - Understand the input
- Decoder - Generate output tokens

There are transformer models which consist of both parts, encoder and decoder, and there are also models which are only an encoder or decoder.
# Positional encoding
For input for a transformer model we need to use the positional encoding which is explained here - [[Positional encoding]].
# Architecture
Transformer architecture looks like that:
![[2 - Images/Transformer/Screenshot 1.png]]

It consists of the following layers and operations:
- Multi-Head Attention ([[Neural Network - Multi-Head Attention (MHA) layer|link]])
- Add & Norm - Residual connection ([[Residual connection|link]]) and Layer Normalization ([[Neural Network - Layer Normalization|link]])
- Feed Forward - A neural network with dense layers ([[Neural Network|link]], [[Neural Network - Fully-connected (dense) layer|link]])
- Linear - A linear layer which performs a linear transformation:
$$
f(x) = Wx + b
$$
	where $W, b$ are trainable parameters. Its output $z = \{z_i\}_{i=1}^m$ is a vector whose elements are called logits.
- Softmax - The softmax function to convert logits into probabilities (values between 0 and 1, such that all of them sum up to one)
## Encoder
Encoder is the first part of a transformer model, on the left-hand side of the picture above. 

It consists of N blocks where each block contains a sequence of neural network layers and additional operations:
- Multi-Head Attention
- Add & Norm
- Feed Forward
- Add & Norm

Output from one block is an input for another block.
## Decoder
Decoder is the second part of a transformer model, on the right-hand side of the picture above. 

It consists of N blocks where each block contains a sequence of neural network layers and additional operations:
- Multi-Head Attention
- Add & Norm
- Multi-Head Attention
- Add & Norm
- Feed Forward
- Add & Norm

Output from one block is an input for another block.
## The final output
Output of the decoder is passed to the linear layer which outputs so called logits $z = \{z_i\}_{i=1}^m$ (values between $-\infty$ and $\infty$).

Logits are passed into the softmax function what gives the final output $y = \{y_i\}_{i=1}^m$ :
$$
\Large
y_i = \text{softmax}(z)_i = \frac{e^{z_i}} {\sum_{j=1}^m e^{z_j}}
$$
where each $y_i$ represents probabilities, those are values between 0 and 1, and they sum up to one.
# Generating tokens
Let's assume, that:
- $\large t^{(\text{in})}_1, \ldots, t^{(\text{in})}_n$ - Given sequence of input tokens
- $\large \{t_i\}_{i=1}^m$ - Set of all possible tokens

Transformer model is used to generate output tokens one by one, recursively. At each step, it outputs probabilities which are used to choose which token should appear next in the sequence.

In the $t$-th step, when generating the $t$-th output token $\large t^{(\text{out})}_t$, transformer model takes as an input:
- The given sequence of input tokens
- All output tokens generated so far $\large t^{(\text{out})}_1, \ldots, t^{(\text{out})}_{t-1}$ 
and outputs a vector with probabilities:
$$
\large y = \{y_i\}_{i=1}^m = \text{Transformer}
( t^{(\text{in})}_1, \ldots, t^{(\text{in})}_n,
t^{(\text{out})}_1, \ldots, t^{(\text{out})}_{t-1} )
$$
where:
- Transformer - A function representing the transformer model (including both encoder and decoder, the final linear layer and softmax after decoder blocks)
- $y_i$ - A probability that the $i$-th token $\large t_i$ out of all possible tokens should be the next generated $t$-th token $\large t^{(\text{out})}_t$ given all the input tokens and output tokens generated so far

This set of probabilities defines a conditional probability mass function ([[Conditional probability distribution function - Discrete random variables|link]]) of a random variable $t$ which represents tokens given all the input tokens and output tokens generated so far.

So we can write:
$$
\large y_i = P(t = t_i \mid t^{(\text{in})}_1, \ldots, t^{(\text{in})}_n,
t^{(\text{out})}_1, \ldots, t^{(\text{out})}_{t-1} )
$$
We can use those probabilities to generate tokens. For example, when generating the $t$-th output token $\large t_t^{(\text{out})}$, we can choose for this token the token which has the highest probability to be the next one.

To generate output tokens, we can use two architectures:
- Use both encoder and decoder
- Use only decoder
## Encoder and decoder
If we use both encoder and decoder, then in the $t$-th step, when generating the $\large t^{(\text{out})}_t$ token, encoder takes as an input the input sequence:
$$
\large t^{(\text{in})}_1, \ldots, t^{(\text{in})}_n
$$
and decoder takes as an input both:
- Encoder's output
- Output tokens generated so far:
$$
\large t^{(\text{out})}_1, \ldots, t^{(\text{out})}_{t-1}
$$
The decoder's first attention layer takes as an input only the tokens generated so far and based on that calculates Query, Key and Value vectors (Q, K, V).

The second attention layer, takes as an input both:
- Encoder's output
- Output from the decoder's first attention layer with Add & Norm

Q, K and V vectors are calculated using different inputs:
- Q - Output from the decoder's first attention layer with Add & Norm
- K and V - Encoder's output
## Decoder only
If we use only a decoder, then in the $t$-th step, when generating the $\large t^{(\text{out})}_t$ token, decoder takes as an input both all input tokens and all output tokens generated so far:
$$
\large t^{(\text{in})}_1, \ldots, t^{(\text{in})}_n,
t^{(\text{out})}_1, \ldots, t^{(\text{out})}_{t-1}
$$
It is an input for the first attention layer.
# Training
How we train a transformer model depends on whether we use encoder or not.
## Encoder and decoder
### Assumptions
Let's assume, that we have a source sequence:
$$
\Large t^{(s)}_1, \ldots, t^{(s)}_{T_s}
$$
and target sequence:
$$
\Large t^{(t)}_1, \ldots, t^{(t)}_{T_t}
$$

For example, source and target sequences can be a question and an answer or text in a source language and target one (for translation).
### Inputs
If we use both encoder and decoder, then:
- Encoder takes as an input the source sequence
- Decoder takes as an input the encoder's output and the target sequence shifted to the right, that is:
$$
\Large \text{<BOS>}, t^{(t)}_1, \ldots, t^{(t)}_{T_t}
$$
	where \<BOS> is a special token indicating the beginning of a sequence. 

Decoder's input are the true tokens, not ones generated by the model. 

Also, we use the causal masking so the model doesn't take into account tokens not generated yet, as described in the next section.
### Masking
We will use the causal masking ([[Neural Network Attention layer - Masking|link]]) to prevent the decoder from taking into account the future tokens, which were not predicted yet, when predicting tokens. 

So when model tries to predict the $t$-th token $\large t^{(t)}_t$, it takes into account only tokens $\large t^{(t)}_1, \dots, t^{(t)}_{t-1}$
### Generating tokens
As explained in the previous section about generating tokens, decoder outputs probabilities which are used to generate output tokens one by one. 

In case of training, in the $t$-th step, it outputs a vector 
$$
y = \{y_i\}_{i=1}^m
$$
where $y_i$ is a probability that the $i$-th token $t_i$, out of all possible tokens $\large \{t_i\}_{i=1}^m$ , is the true $t$-th target token $\large t^{(t)}_t$ given all input tokens and previously generated tokens:
$$
\Large y_i = P(t^{(t)}_t = t_i \mid t^{(s)}_1, \ldots, t^{(s)}_{T_s},
t^{(t)}_1, \ldots, t^{(t)}_{t-1} )
$$
### Training using MLE
We can train the model using the maximum likelihood estimation (MLE) ([[Maximum Likelihood Estimation (MLE)|link]]). In that case, if $t_i$ is the true target token $\large t^{(t)}_t$, then we want to maximize the probability $y_i$ predicted by the model that this is the true token.

MLE is equivalent to minimizing the negative log-likelihood, which we can achieve using the cross-entropy loss ([[Relation of Cross-Entropy to the Maximum Likelihood Estimation|link]], [[Cross-Entropy for classification|link]]).
### Calculating loss
When making predictions for every token $\large t^{(\text{out})}_t$ , we calculate a loss for that one token $L_t$ using generated probabilities $\large y = \{y_i\}_{i=1}^m$. 

Total loss is a sum of losses for all tokens:
$$
\Large L = \sum_{t=1}^{T_t} L_t
$$
## Decoder only
In case when we use only a decoder, training is almost the same as in case when we have additionally an encoder, like described in the previous section.

The difference is that we don't have separate source and target sequences but only one sequence of tokens which is an input for the model:
$$
\large t_1, \ldots, t_{T}
$$

The same sequence shifted to the left:
$$
\large t_2, \ldots, t_{T}, \text{<EOS>}
$$
is used as a target sequence which model tries to predict. Here \<EOS> is a special token indicating end of sequence (indicating that there shouldn't be any more tokens generated).

Model predicts the next token based on the previous tokens:
- Predict $t_2$ based on $t_1$ 
- Predict $t_3$ based on $t_1, t_2$ 
- ...
- Predict $t_{T+1} = \text{<EOS>}$ based on $t_1, \dots, t_T$ 

So, when predicting the $t$-th token $\large t_t$ , model outputs probabilities 
$$
\large y = \{y_i\}_{i=1}^m
$$
where $y_i$ is a probability that the $i$-th token out of all possible tokens $\large \{t_i\}_{i=1}^m$ is the true token $\large t_t$ given all the tokens generated so far:
$$
\large y_i = P(t_t = t_i \mid t_1, \ldots, t_{t-1})
$$
### Training for questions and answers (not predicting all the tokens)
When using only a decoder, we might not be interested in predicting all the tokens. For example, when we have a question and we want to generate an answer, we don't need to predict tokens from the question, only the answer.

When training a transformer model in such a case, we still predict all the tokens (including the question) but they are not included in the loss (they don't make loss any bigger or smaller).

We still predict all the tokens so we don't need to change the transformer architecture. Creating separate architecture for such a case would be complicated and it is not needed.

During training we perform some unnecessary calculations because of that (predicting tokens we don't care about) but computational cost of that is very small compared to the cost of the entire training.

Even if we didn't make predictions for those tokens, they would will still have an impact on calculations because we would still calculate for them Q, K and V vectors in the attention layer. That is very expensive operation computationally and making additional predictions is very little compared to that.

#MachineLearning 