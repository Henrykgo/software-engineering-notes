Retrieval works by ranking chunks(documents) based on their relevance to a given query. Retrieval algorithms differ with the way they calculate this relevance. In [[RAG]] this is the step that decides what the model gets to see.
### Term-based retrieval
Ranks chunks by how many of the query's words they contain, weighting each word by how rare it is. It matches words at the lexical level, not the semantic level, so it is fast and precise but blind to synonyms.
#### How it works:
1. When indexing, create an inverted index e.g. mapping terms to documents that contain them and their frequency etc (like index in the back of a book)
2. When a query arrives the model will retrieve all the chunks that contain those words
3. Score each collected chunk. Two things that matter:
	- Term  frequency (TF): how often a term appears in a chunk. More is better.
	- Inverse document frequency (IDF): a terms importance is inversely proportional to the number of documents it appears in. e.g. the word "The" is worth nothing
4. return the top scoring chunks
TF-IDF is the basic scoring formula. BM25 is the improved version used by most search engines, such as Elasticsearch.

### Embedding-based retrieval
Relevance is measured by how close the chunk's meaning is to the query's meaning. An embedding is typically a vector that tries to save the important properties of the original data.
#### How it works:
1. When indexing, pass every chunk through an [[Embeddings]] model and store the vector it produces in a vector database.
2. When there is a query, pass it through the same model to get a query vector.
3. [[Vector search]]: Find the stored vectors closest to the query vector (closeness usually measured by cosine similarity).
4. return the chunk those vectors belong to.

For smaller datasets we can look at every vector however for bigger dataset this would be too slow. For larger dataset vector search is usually done using an approximate nearest neighbour algorithm (what is this?). 

### Comparing the 2

|            | Term-based                            | Embedding-based                                                               |
| ---------- | ------------------------------------- | ----------------------------------------------------------------------------- |
| Matches on | words                                 | meaning                                                                       |
| Cost       | cheap, no model                       | embedding call per chunk and per query                                        |
| Good at    | exact terms: names, codes, rare words | synonyms, paraphrase                                                          |
| Bad at     | synonyms, meaning                     | exact keywords, words with no meanings such as a product ID/invented username |
| Example    | Elasticsearch, BM25                   | embedding model + vector database                                             |

### Hybrid Retrieval
Given that different retrieval algorithms have different pros/cons a production system usually combines several approaches. A hybrid search combines both of the above.
Sequential: First use a cheaper term based retriever and fetch those candidates, and then use a more precise embeddings based retriever on those candidates.
Ensemble: Run both retrievers on both sets and then use the algorithm RRF that merges the two ranked lists by rank position (no need to normalise).
## Sources
- AI Engineering, Chip Huyen, chapter. 6, "Retrieval algorithms" p





