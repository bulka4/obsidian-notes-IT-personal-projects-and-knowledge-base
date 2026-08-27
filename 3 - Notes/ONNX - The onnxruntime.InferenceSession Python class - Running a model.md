Tags: [[_ONNX]] [[__Machine_Learning]]
#ONNX #MachineLearning 

# `session.run()`
To run a model, we can use the following code:
```python
import onnxruntime as ort

session = ort.InferenceSession("model.onnx")

outputs = session.run(
    None,
    {"input_ids": input_ids}
)
```

`InferenceSession` loads the ONNX computational graph and prepares it for execution, and `session.run()` executes it and generates an output.
# Using `InferenceSession` for token generation
In order to use `InferenceSession` for token generation, we need to call it multiple times in a loop because when we call it one, it generates only one next token (as explained earlier in the "Example model outputs > Logits" section).

Example code:
```python
import numpy as np
import onnxruntime as ort
from transformers import AutoTokenizer

tokenizer = AutoTokenizer.from_pretrained("gpt2")

session = ort.InferenceSession("model.onnx")

text = "The customer information is stored"
inputs = tokenizer(text, return_tensors="np")

input_ids = inputs["input_ids"]

for _ in range(20):
    # Run the ONNX model
    outputs = session.run(
        None,
        {
            "input_ids": input_ids
        }
    )

    # [batch, sequence_length, vocabulary_size]
    logits = outputs[0]

    # Get predictions for the next token
    next_token_logits = logits[:, -1, :]

    # Simplest generation strategy: choose highest-scoring token
    next_token = np.argmax(
        next_token_logits,
        axis=-1
    )

    # Add the generated token to the sequence
    input_ids = np.concatenate(
        [input_ids, next_token[:, None]],
        axis=1
    )

    # Stop if EOS token was generated
    if next_token[0] == tokenizer.eos_token_id:
        break

# Convert token IDs back to text
generated_text = tokenizer.decode(
    input_ids[0],
    skip_special_tokens=True
)

print(generated_text)
```