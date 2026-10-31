Log-structured merge-tree is a storage engine design that collects writes in a in memory sorted structure (memtable), writes it out of to disk as a sorted immutable segment file (SSTable) once it fills up, and merges those files in the background through compaction. Keeping the segments sorted is what makes merging cheap and allowing a sparse index.

## How it works?
1. A write is appended to the [[Write-ahead log]] (WAL), then inserted into the memtable (sorted, in memory)
2. When the memtable reaches it size limit, its written out to disk as a new [[SSTable]]; the log is discarded and a fresh memtable starts.
3. A read checks the memtable first and then each SSTable from the newest to oldest. It uses a [[Bloom Filter]] to skip files that cannot contain the key.
4. In the background compaction merges SSTables keeping the newest value value per key and discarding overwritten and tombstoned keys.
### Tombstone
An append only log cannot delete a key and its values, so a delete appends a special deletion record called a tombstone. During compaction the tombstone tells the merge to discard any previous values for that key. Once the tombstone is merged into the oldest segment it can be dropped.
### Compaction
Merging several segments files into one, keeping only newest value for each key and dropping overwritten and deleted records. Many LSM-based storage systems allow you to configure which compaction strategy to use, with 2 common ones below:
##### Size-tiered compaction
Newer, smaller SSTables are repeatedly merged into older, larger ones, so the oldest files grow very big and merging them requires a lot of temporary disk space. It can handle very high write throughput because most data is rewritten only a few times, in large sequential merges.
##### Leveled compaction 



### Used in?
This algorithm (LSM storage Engines) are used in: RocksDB, Cassandra, ScyllaDB and Hbase all of these were inpsired by Google's Bigtable paper (introduced terms such as SSTable and memtable).


## Compare with
[[B-trees]]: update-in-place alternative

## Tradeoffs



### Source
- DDIA (Chapter 4. Storage and retrieval) #source/ddia/ch4