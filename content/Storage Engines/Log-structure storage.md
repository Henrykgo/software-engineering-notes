Log is an append-only file for storing data. A log-structured storage engine uses logs as its main storage format.

Updates are not performed in place: each write is appended to the end of the log as a new record, and because earlier records are never overwritten, the current value of a key is the last occurrence of it. Deletes are represented by a [[LSM-Trees#Tombstone|Tombstone]]. Old and overwritten data is removed later by [[LSM-Trees#Compaction|Compaction]].
### Implementations:
[[LSM-Trees]]: the main log-structured storage engine design: based on merging and compacting sorted files ([[SSTable]]).
### Tradeoffs:
**+** : Sequential writes, so very high write throughput
**+** : Immutable files make crash recovery and concurrency simpler
**-** : Old values remain until cleanup, so disk usage is higher than the live data
**-** : A keys current value is not in one fixed place, so reads have more work to do
