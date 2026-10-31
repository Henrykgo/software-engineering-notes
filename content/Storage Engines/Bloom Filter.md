A bloom filter is a space-efficient probabilistic data structure that quickly checks on whether an element might exist in a set.

![[Screenshot 2026-10-20 at 15.02.49.png]]
### How does it work?
1. Start with a bit array (bloom filter) of size `m`, all 0s, and `k` hash functions.
2. To insert a key, run it through each hash function. Each gives an index into the array. 
3. Set the bit at each of those k indexes to 1.
4. To check if a key is in the bloom filter, hash it the same way and look at the k bits.
5. If any bit is 0, the key is definitely not in the set.
6. If all are 1, they key is possibly in the set. Other keys may have the same bits, which can lead to false positives. 



### Sources
- DDIA (Chapter 4. Storage and retrieval) #source/ddia/ch4