A foundation model is a large, general-purpose model that many applications are built on.

### From language models to foundation models

**language model**: predicts the next token given the previous one. A token is the unit: a word, part of a word or character. Two kinds:
- masked: predicts a token from both sides (BERT)
- Autoregressive: predicts the next token in a sequence using only the preceding tokens, this is good for generating text and is used by nearly all current models

**Large language model**: The same thing scaled up in data and parameters. This scaling was possible because pre-training is self-supervised ([[Types of learning]]), any text is training data, so there is no labelling bottleneck.

**Foundation model**: A large, general purpose model, often multimodal (different type of data) that serves as a base many applications use. This can be done with prompt engineering, RAG or finetuning.