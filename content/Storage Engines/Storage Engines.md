A storage engine decides how a database is stored both in memory and on disk, which determines what reads and writes cost.
### Transactional Processing (OLTP) vs Analytics (OLAP)
These 2 require very different engines
- **OLTP**: optimised for a high volume of requests, each reads and writes a small number of records and needs fast responses. Records typically accessed by a primary key or secondary index. These indexes are usually ordered mappings from key to record supporting range queries.
- **OLAP(Data warehouses and similar)**: optimised for complex read queries that scan a large number of records. A column-oriented storage is used as well as compression to minimise the amount of data that such queries need to read off disk and uses JIT compiled queries or vectorisation to minimise CPU time spend of processing data.

### Log-Structured approach vs Update-in-place approach
- The [[Log-structure storage|log-structure approach]] only supports appending files and deleting files but never updates a file that is already written. They usually have high write throughput. The [[LSM-trees]] is the main design here, built from SSTables, its used by: LSM-trees, RocksDB, Cassandra, Hbase, ScyllaDB, Lucene and more.
- The update in place approach looks at the disk as a set of fixed-size pages that can be overwritten. The most common example of this is [[B-trees]], and are used by all major relational OLTP databases and many non-relational ones. B-trees tend to be better for reads, providing higher read throughput and lower response times.