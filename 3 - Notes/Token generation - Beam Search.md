Tags: [[__Machine_Learning]]

# Introduction
Beam Search is a technique used when generating tokens ([[Token generation|link]]), to achieve better quality.

Each token a model generates, has an impact on what tokens will be generated next. Beam Search helps with a problem, when model predicts one bad token and that causes all the further tokens to be generated badly.

Instead of generating one sequence, with Beam Search we generate K sequences and we choose those, where probability of all the tokens in total is the highest.

Number K is called a beam width and each sequence is called a beam.
# How it works
***1. Expand each beam*** 
For every beam, find K tokens, which are most likely to be the next token for that beam.

Convert each beam into K new beams, each containing 1 additional token out of the K most likely tokens we found.

If we are starting and beams doesn't have any tokens yet, then in this step we just generate K beams, each one with one token.

If we have already K beams with some tokens:
- beam 1: $\large t_{11}, \ldots, t_{1n}$ 
- ...
- beam K: $\large t_{K1}, \ldots, t_{Kn}$ 
then every beam generates K new candidate sequences, for example beam i generates:
$$
\large \begin{gather}
& t_{i1}, \ldots, t_{in}, t_{i n+1}^{(1)} \\
& \vdots \\
& t_{i1}, \ldots, t_{in}, t_{i n+1}^{(K)} \\
\end{gather}
$$
For each beam we will have a new set of candidate tokens $\large t_{i n+1}^{(1)}, \dots, t_{i n+1}^{(K)}$ because probability of those tokens depend on tokens which we already have in beams, and different beams have different tokens.

***2. Score all the beams***
For every beam j, calculate a score:
$$
\large
\text{score} = \sum_{i=1}^{n+1} \log P(t_{ji} \mid t_{j,<i})
$$
where:
- $P(t_{ji} \mid t_{j,<i})$ - Probability of the $t_{ji}$ token given all the previous tokens $\large t_{j1}, \dots, t_{j i-1}$ 

So highest scores are assigned to beams where probability for all the tokens in total is the highest.

***3. Keep only the top K beams***
Now we have $K^2$ beams. Out of them, we choose K beams with the highest scores.

***4. Repeat***
We repeat this process until we generate the EOS token (indicating the end of sentence) or when the max length is reached.

#MachineLearning 