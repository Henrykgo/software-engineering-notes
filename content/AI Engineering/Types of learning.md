How a model learns depends on what signal it gets.

### Supervised Learning
Learn from labelled examples: an input paired with the correct output.
In LLMs: supervised finetuning (SFT) trains the model on (prompt, response) pairs written by humans, so it learns to answer instead of continuing text.

### Self-supervised learning
The model infers labels from the input data itself, so nothing needs human labelling. This is what removed the data-labelling bottleneck and let language models scale into LLMs.
In LLMs: pre training. Each input sequence provides both the labels (tokens to be predicted) and the context to predict them from, so one sentence gives several training samples.

| Input (context)              | Output (next token) |
| ---------------------------- | ------------------- |
| `<BOS>`                      | I                   |
| `<BOS>` I                    | love                |
| `<BOS>` I love               | street              |
| `<BOS>` I love street        | food                |
| `<BOS>` I love street food   | .                   |
| `<BOS>` I love street food . | `<EOS>`             |

`<BOS>` and `<EOS>` mark the start and end of a sequence. 

### Unsupervised learning
Labels are not needed.

### Reinforcement learning
Trains a model by giving it feedback scores (rewards) instead of fixed correct answers. (model learns to produce answers that get higher score over time).
In LLMs: RLHF (reinforcement learning from human feedback) A model is trained using a reward model learned from human comparisons, and then optimised to produce responses human prefer.