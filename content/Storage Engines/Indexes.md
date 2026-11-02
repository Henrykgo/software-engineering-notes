An index is an additional structure derived from the primary data and introduces additional overhead. 

### Tradeoffs
Indexes help to speed up reads but with a trade off: they require additional disk space and can slow down writes (as the index needs to be updated whenever the underlying data changes).
### Implementations
- [[LSM-Trees]]: log structured, append-only segments merged in background
- [[B-trees]]: updated-in-place, fixed-size pages
### Source
- DDIA (Chapter 4. Storage and retrieval) #source/ddia/ch4