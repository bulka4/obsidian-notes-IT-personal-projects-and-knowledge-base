Tags: [[__Machine_Learning]]

# Introduction
Sometime we perform many iterations of sending a prompt and generating tokens based on it, and subsequent prompts are related to the previous ones, for example when we ask multiple related questions to a chatbot, make a conversation.

In that case, when generating a response for a prompt, it is needed to take into account not only that prompt but also previous ones.

Context window determines how many past prompts we take into account when generating a response.