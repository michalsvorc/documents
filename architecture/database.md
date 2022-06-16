# Database

Topics:

- [ACID](https://en.wikipedia.org/wiki/ACID)
- [CAP theorem](https://en.wikipedia.org/wiki/CAP_theorem)

DB can become a bottleneck because there is an upper limit to how many concurrent read/write you can perform.

DB must choose between availability and consistency (in CAP) in most cases.

## Performance

- Indexing: column based, slow down reads, more storage required
- Denormalization: move redundant data to separate tables, risk of data inconsistency across tables
- Connection Pooling: allow multiple application thread to use same DB connection
- Caching: cache sits in front of the database

### Read replicas

- Create replica servers to handle reads
- Master node dedicated only to writes
- Increases fault tolerance in case of multiple read replicas

## Horizontal partitioning (sharding)

- [geeksforgeeks.org](https://www.geeksforgeeks.org/database-sharding-a-system-design-concept/)

- Schema of the table stays the same, but is split across multiple DBs
- Downsides: Hot keys in one shard, no joins across shards

Database shards are autonomous; they don’t share any of the same data or computing resources. In some cases, though, it
may make sense to replicate certain tables into each shard to serve as reference tables.

## Vertical partitioning

- Divide schema into separate tables
- Best when most of the data in the row is not needed in frequent queries

## NoSQL

- [Wikipedia](https://en.wikipedia.org/wiki/NoSQL)
- [SQL vs NoSQL - medium.com](https://medium.com/must-know-computer-science/system-design-sql-vs-nosql-4cdfb9f53d69)

SQL data is normalized, meaning minimized data duplication across different tables.

SQL database can be scaled vertically (horizontal scaling is complicated), NoSQL can be scaled both horizontally and
vertically.

Many NoSQL stores compromise consistency in favor of availability, partition tolerance, and speed. Most NoSQL databases
offer a concept of "eventual consistency", in which database changes are propagated to all nodes "eventually" (typically
within milliseconds), so queries for data might not return updated data immediately.

Data structures of NoSQL databases:

- Key–value: Dynamo, Redis, ZooKeeper
- Document: Apache CouchDB, Couchbase, MongoDB
- Wide column: Cassandra, ScyllaDB, HBase
- Graph: Apache Giraph, Neo4J, OrientDB

## Wide column databases

The values of single column databases are stored contiguously. Each row can have a different number of columns.

They deliver high performance on aggregation queries like SUM, COUNT, AVG, MIN, etc. as the data is readily available in
a column.
