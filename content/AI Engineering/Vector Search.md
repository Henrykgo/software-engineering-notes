A vector database stores vectors. Vector search finds the stored vectors closest to a query vector in a vector database and returns them. An exact search in a vector will have to look at every vector, so in a database with a 1000 vectors is fine however in a database with over 1 million vectors it can be slow.
For larger datasets, vector search is usually done using an approximate nearest neighbor (ANN) algorithm.
#### ANN algorithms
ANN algorithms organise the vectors so that only certain regions are searched (spliting them into buckets, trees or graphs)
some examples:
- LSH(locality-sensitive hashing): hashing similar vectors into the same buckets to speed up similarity search, trading some accuracy for efficency.
- HNSW(Hierarchical Navigable Small World): multi-layer graph where nodes represent vectors and edges connect similar vectors
(can add more in the future)
