Oranizing into services taught teams not to trust each other in most of the same ways they are not supposed to trust external developers.

what did work well for Amazon, though, was the element of organizational change that came from being wholeheartedly service based. Service teams think of their software as being a cog in a far larger machine. 

Be of the web, not behind the web.

your users weren't just customer ot businesspeople; they were other applications, and they really cared that your service was reliable. So applications became platforms, and building platforms is hard.

LinkedIn felt this pain as it evolved away from its original, monolithic Java app into 800-1,100 services. Complex dependenies led to instability, versioning issues caused painful lockstep relaeses, and early on, it wasn't clear that the new architecture was actually an improvement.

On difference in the way LinkedIn evolved it approach was its use of a messaging system built in-house: Kafka. Kafka added an asynchronous publish=subscribe model to the architecture that enabled trillions of messages a day to be transported around the organization.

Replayable logs, like Kafka, can play a role of an event store: a middle ground between a messaging system and a database. Replayable logs decouple services from one another. they also provide a centrial point of storage that is fault-tolerant and scalable - a shared source of truth that any application can fall back to.

A shared source of truth turns out to be a surprisingly useful thing. Microservices, for example, don't share their databases with on another.

Replayable logs is purely about storing data and pushing it to somewhere new. This idea of pure data movement is important, because data on the outside - the data services share - is most tightly coupled of all, and the more services an ecosystem has, the more tightly coupled this data gets. The solution is to move data somewhere that is loosely coulped, so that means moving it into your application where you can manipulate it to your heart's content. So data movement gives applications a level of operabilty and control that is unachievable with direct, runtime dependency. This idea of retaining control turns out to be important - it's the same reason the shared database pattern doesn't work out well in practice. 

So, this Replayable log-based approach has two primary benefits. 

First, it makes it easy to react to events that are happening now, with a toolset specifically designed for manipulating them.

Second, it provides a central repository that can push whole datasets to whatever they may be needed. 

Database-centric approach works wonderfully for indiviual application, But we don't live in a world of indiviual application. We live in a world of interconnected systems 

We need a mechanism for sharing data that complements this complex, interconnected world. Events lead us to this. They constantly push data into out applications. These applications react, blending streams together, buildign views, changing states, and moving themselves together. In streaming model there is no shared database. The database is the the eventstream, and the application simply molds it into something new.