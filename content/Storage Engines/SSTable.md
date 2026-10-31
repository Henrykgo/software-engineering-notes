Sorted Strings Table is a file that stores key-value pairs sorted by key, with each key appearing only once.

### Why are they used?
- **Efficient reads**: keys are sorted, so finding a key is fast
- **Less memory usage**: a sparse index stores only some keys
- **Efficient range queries**: sorted keys make scanning a range of keys easy
- **Compression**: data can be compressed to save disk space

![[Screenshot 2026-10-23 at 08.43.48.png]]

### How are SSTables merged?
Because each SSTable is sorted by key, merging works similarly to merge sort: read the files side by side, copy the next sorted key in sorted order into the output, and if a key appears in multiple files, keep only the value from the newest segment. This runs in background as compaction, covered in [[LSM-Trees]].

### Part of
[[LSM-Trees]]: The memtable is flushed to disk as an SSTable, and compaction merges SSTables.


### Source
- DDIA (Chapter 4. Storage and retrieval) #source/ddia/ch4