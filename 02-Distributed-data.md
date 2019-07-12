In the name of
- **scalability** (too much data to fit in one machine)
- **high availablity** (redundancy is good! 😂so you can rest assured even a datacenter is burned down, you data has replicates somewhere else)
- **low latency** (geolocation wise, you need to put data in different zones around the world to serve users faster, physical distance always rules 🥶)

we need distributed data. And we need them in at least 2 ways: **replication** & **partition(sharding)**.

# Replication
The main difficulty of replication is handling *changes* to replicated data. We have 3 ways to handle this: *single-leader*, *multi-leader* & *leaderless*.

## Single Leader

### Data flows
read-write-queries -> leader node -> replication stream => replicas (follower nodes) <- read-only-queries

- writes are only accepted by leader node
- reads can read from leader or follower

This mode is build-in for many relational dbs such as *Postgres*, *MySql* or *Oracle*, and also for nonrelational dbs as *MongoDB*, *RethinkDB*, *Espresso*. *Kafka* & *RabbitMQ* as message brokers also support the single leader mode.

### Synchronous and asynchronous
When you use this mode, we decide between sync & async replications:
- *Semi-synchronous*: you can make *one* follower with synchronous replication, and other nodes asynchronous. That means you make sure the data is available at least on leader & *one* follower, and other nodes can use asynchronous replication.
- complete asynchronous: it's common to make the replica completely async, then you can continue process write even *all* the replication failed, but this also causes weak durability (leader一挂就有可能全部挂掉了). 




