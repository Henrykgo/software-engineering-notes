When a model gives a response that is not grounded in facts.

### Why does it happen?
2 hypotheiss
1. A language model hallucinates because it cannot differentiate between the data it is given and the data it generates. 
- e.g. you give the model the prompt "who is Henryk?", the first sentence the model generates is "Henryk is an writer", so the next token generated will be conditioned on the sequence "Who is Henryk? Henryk is a writer". The model treats "Henryk is a writer", something it has produced the same way it treats a given fact.

2. Knowledge mismatch: During supervised finetuning the model imitates answers written by labellers. If a labeller uses knowledge the model doesn't have, we are essentially teaching the model to hallucinate. 

### How to try and prevent Hallucination?
- Ground the answer: put the relevant information in the prompt so the model doesnt have to recall it([[RAG]])
- provide verification: for each response ask the model to retrieve the sources it based the response on
- Lower temperature for factual tasks
- shorter answers since more tokens mean more chances to hallucinate 
- Training: reward the model for admitting uncertainty rather than guessing e.g. adding prompts like: “Answer as truthfully as possible, and if you’re unsure of the answer, say, ‘Sorry, I don’t know.’”

### How to prevent for RAG?
- Instruct the model to use only the retrieved chunks
- require citation for every claim and reject claims whose citations do not match a retrieved chunk
- refuse when retrieval returns nothing relevant

### Detection (Factual consistency)
- local: check the answer against the context it was given (important for summarization)
- global: check against open knowledge (for chat bots, market research)


Sources
chapter 2, 4