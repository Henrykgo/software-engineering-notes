A WAL is an append-only disk log that records changes before they are applied to data pages providing crash recovery by replaying the log (REDO).

### How it works
1. Changes are recored in the WAL, flushed to permanent storage before writing the changes to the data files.
2. Data pages do not have to be flushed to disk at every transaction commit, because the WAL allows changes to be recovered from a crash.
3. After a crash, the database replays the WAL to recover the changes that are not yet applied to data pages.

### Why it is efficient?
- reduces I/O operations as only the WAL needs to be flushed on every commit, rather than every data file changes by the transaction.

### Other uses
- **point-in-time recovery**: restore a back up up to a certain chosen time
- **replication**: ship WAL records to replicas to reproduce changes

### Used by
- **B-trees**: support recovery after a crash during page updates/splits
- **LSM-trees**: recover in memory memtable changes that were not yet flushed to SSTables

Key words:
Flush: force data from a temporary buffer in memory to permanent storage (disk/SSD)
### Sources
- DDIA (Chapter 6. Replication) #source/ddia/ch6
- Postgres docs/wall #source/postgresql/wal
