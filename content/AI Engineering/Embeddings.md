An embedding is a vector that represent a piece of data so that similar meanings end up close together in the vector space. There are models that are trained to create embedding: e.g. open source models such as BERT or CLIP.

#### How it works?
- text goes into an embedding model and a vector of a few 100/1000 numbers come out
- similar texts produce vectors that are close (measured by cosine similarity or dot product)

#### Used for
- retrieval: embed chunks and queries, find the nearest [[Retrieval]], [[Vector Search]]
- semantic similarity: how close the generated response is to the reference response in meaning

#### Multimodal
- A joint model such as CLIP embeds text and images into the same space, so a text query can retrieve an image directly.  Another solution is to caption images and embed the captions.

Sources
chapter 3 and 6

