Storing the values of each column together rather than storing all the values of each row together (like shown below).

![[Screenshot 2026-10-23 at 08.01.47 1.png]]

### Why is it useful?
In a data warehouse a fact table usually has 100 or more columns, but a typical query accesses only 4 or 5 of them at one time. A row-oriented query has load every query from disk compared to loading just the columns needed.

### Column Compression
![[bitmap-index storage.png]]


### Source
- DDIA (Chapter 4. Storage and retrieval) #source/ddia/ch4 
