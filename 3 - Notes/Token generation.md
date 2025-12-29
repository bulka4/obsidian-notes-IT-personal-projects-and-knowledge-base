Tags: [[__Machine_Learning]]

# Introduction
Token generation is a task when model generates a sequence of tokens. Those tokens can be:
- Words
- Actions, steps in a plan
- Elements in a DNA (amino acids or nucleotides)
- Image (multipixel part of an image)

Model is predicting recursively the next token, considering tokens which were already generated. It stops when the special 'end' token is generated or the max length is reached.
# Techniques
There are multiple techniques which can improve the process of generating tokens which are described here - [[Token generation - Techniques]].

#MachineLearning 