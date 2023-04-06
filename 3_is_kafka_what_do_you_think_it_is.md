Kafka is like REST but asynchronous
=

Kafka provides an asynchronous protocol for connecting programs together, but it is undoubtedly a bit different from TCP, HTTP or RPC. The difference is the presence of a broker. A broker is a separate piece of infrastructure that broadcasts message to any programs that are interested in them, as well as storing them for as long as is needed.

Another use case is request-response. You can build this type of request-respone interaction with Kafka using two topics: one that transports the request and one that transaport the response.

So this leaves the question: would you be better off using a stateless protocol like HTTP?

So, Kafka is a mechanism for program to exchange information, but its home groung is event-based communitcation.

Kafka is like Service Bus?
=
Kafka, howerver, is a streaming platform, and as such puts emphasis on high-throughtput event and streaming processing. A Kafka cluster is a distributed system a heart, provviding high availabilty, storage, and linear scale-out. This quite different from traditional messaging systems, which are limited to a single machine, or if they do scale outward, those scalabilty properties do nt stretch from end to end. Tools like Kafka Streams and KSQL allow you to write simple programs that manipulate events as they move and evolve. These make the processing capabilities of a database available in the application layer, via an API and outside the confines of the shared broker.

one single Kafka cluster at the center of an organization is quite common, the pattern works because it is simple. nothing more than data transfer and storage, provided at scale and high availablity.

kafka is like database
=
It provides storage; production topics with hundreds of terabytes are common. It has SQL interface that lets users define querues and execute them over the data held in the log. Kafka streams are optimized for continual computation rather than batch processing.
Kafka is designed to move data, operating on the data as it does so. It's about real-time processing first, long-term storage second.

What is Kafka really? A Streaming platform
=
Kafka is a streaming platform. At its core sits a cluster of Kafka blockers. 

The blocker's ability to scale, store data, and run without interruption makes it a unique tool for connecting many disparate applications and services across a department or organization.  The Connection interface makes it easy to evolve away from lagacy system, by unlocking hidden datasets and turning them into event streams. Stream processing lets applications and services embed logic directly over these resulting streams of events.