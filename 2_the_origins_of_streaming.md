The mobile device land their data into Kafka, which buffers it until it can be extracted by the various applications that need to put it to further use. For this type of workload the cluster would be relatively large.

After Kafka, There is the streaming processing layer. This is a clustered application, where queries are either defined up front via Java DSL or sent dynamically via KSQL, Kafka's SQL-like stream processing language. Unlike in a traditional database, these queries compute continuously, so every time an input arrives in the stream processing layer, the query is recomputed, and a result is emmited if the value of the query has changed.

The streaming layer is fault-tolerant
=
It runs as a cluster in all available nodes. If one node exits, another will pick up where it left off. Likewise, you can scale out the cluster by adding new processing nodes.

Each steam processor node can hold state of its own
=
This is repuired for buffering as well as holding whole table. This idea of local storage is important, as it lets the stream processor perform fast, message-at-a-time queries without network - a necessary feature for high-velocity workloads seen in internet-scale use cases. But this ability to internalize state in local stores turns out to be useful for number of business-related use cases too.

Each stream processor can write and store local state
=
Making message-at-a-time network calls isn't particularly good idea when you're handling a high-throughput event stream. For this reason stream processor write data locally and back those writes up to Kafka.