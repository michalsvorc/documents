# ElastiCache for Redis

- [Comparing Memcached and Redis](https://docs.aws.amazon.com/AmazonElastiCache/latest/red-ug/SelectEngine.html)
- [Guide](https://docs.aws.amazon.com/AmazonElastiCache/latest/red-ug/WhatIs.html)

## Components and features

- [ElastiCache for Redis components and features](https://docs.aws.amazon.com/AmazonElastiCache/latest/red-ug/WhatIs.Components.html)
- [ElastiCache for Redis terminology](https://docs.aws.amazon.com/AmazonElastiCache/latest/red-ug/WhatIs.Terms.html)

### ElastiCache nodes

A node is the smallest building block of an ElastiCache deployment. A node is a fixed-size chunk of secure,
network-attached RAM. Each node runs an instance of the engine and version that was chosen when you created your
cluster.

### ElastiCache for Redis shards

A Redis shard (called a node group in the API and CLI) is a grouping of one to six related nodes.

- A Redis (cluster mode disabled) cluster always has one shard.
- Redis (cluster mode enabled) clusters can have up to 500 shards, with your data partitioned across the shards.

### ElastiCache for Redis clusters

A Redis cluster is a logical grouping of one or more ElastiCache for Redis shards. Data is partitioned across the shards
in a Redis (cluster mode enabled) cluster.

### ElastiCache for Redis replication

Replication is implemented by grouping from two to six nodes in a shard (in the API and CLI, called a node group). One
of these nodes is the read/write primary node. All the other nodes are read-only replica nodes.

Each replica node maintains a copy of the data from the primary node. Replica nodes use asynchronous replication
mechanisms to keep synchronized with the primary node. Applications can read from any node in the cluster but can write
only to primary nodes.

### ElastiCache for Redis endpoints

An endpoint is the unique address your application uses to connect to an ElastiCache node or cluster.

- Single node endpoints for Redis (Cluster Mode Disabled): An endpoint is the unique address your application uses to
  connect to an ElastiCache node or cluster.
- Multi-node endpoints for Redis (Cluster Mode Disabled): A multiple node Redis (cluster mode disabled) cluster has two
  types of endpoints. Use the primary endpoint for all writes to the cluster.
