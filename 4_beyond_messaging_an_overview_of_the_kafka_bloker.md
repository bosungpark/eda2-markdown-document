A Kafka cluster is essentially a collection of files, filled with different machines.

Originally built to distributed the datasets created by large social networks, Kafka was predominantly shaped by a need to operate at scale, in face of failure.

The underlying abstraction is a partitioned log - essentially a set of append-only files spread over a number of machines - which encourages sequential access patterns that naturally flow with the grain of the underlying hardware.

only the lastest messages matter, to mission-critial use cases where message and their relative ordering must be preserved with the same guarantees as you'd expect from a DBMS or storage system.

The Log
=
At the heart of the Kafka messaging system sits a paritioned, replayable log. Both reads and writes are sequential operations. This makes them sympathetic to the underlying media, leveraging prefetch, the various layers of caching, and natually batching operation together. This turn makes them efficient. The server doesn't even import them into the JVM. Data is copied directly from the disk buffer to the network buffer.

Partitons are a fundamental concept for most distributed data systems. A Partition is just a bucket that data is put into, much like buckets used to group data in a hash table.

Linear Scalabilty
=
Logs provide a hardware-sympathetic data structure for messaing workloads, but Kafka is really many logs, spanning many different machines. The system ties these together, routing messages reliably, replicating for fault tolerance, and handling failure gracefully.

Scaling is thus a pretty simple affair: add new machines and rebalance. Consumption can also be performed in parallel, with messages in a topic being spread over several consumers in a consumer group.

The main advantage of this from an architectural perspective is that it takes the issue of scalabilty off the table.

Scalabilty opens other opportunities too. Single clusters can grow to company scales, without the risk of workloads overpowering the infrastructure.

Segregating Load in Multiservice Ecosystem
=
Service architectures are by definition multitenant. A single cluster will be used by many different services. a single cluster can be shared by many number of services, causing degradation or instability.

Kafka includes a thoughput control feature, called quotas.

Maintaining Strong Ordering Guarantees
=
There is a couple of things that need to be sonsidered to ensure strong ordering guarantees, The first is that messages that required relative ordering need to be sent to the same partition.
Something key-based ordering isn't enough, and global ordering is required. To maintain global ordering, use a single partition topic.

The second thing to be aware of is retries. there is no potential for a reordering of events when failure occur and batches are retried. This is simply something we configured.

Ensuring Messages Are Durable
=
Kafka provides durabilty through replication. This means messages are not be lost, if not every machine fails.


Load-Balance Services and Make Them Highly Available
=
Event-driven services should always be run in a highly available. The main reason for this is it's essentially a no-op

if one of the services fail, Kafka will detect this failure and reroute message from the failed service to the one that remains. If the failed service comes back online, load flips back again.

This process actually works by assigning whole partition to different consumers. A strength of this approach is that a single partition can only ever be assigned to a single service instance(consumer). This is invariant, implying that ordering is guaranteed, even as service fail and restart.

So services inherit both high availablity and load balancing, meaning they can scale out, handle unplanned outages, perform rolling restarts without service downtime. In-fact Kafka releases are always backward-compatible with previous version.

