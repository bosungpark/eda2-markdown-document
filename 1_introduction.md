Oranizing into services taught teams not to trust each other in most of the same ways they are not supposed to trust external developers.

what did work well for Amazon, though, was the element of organizational change that came from being wholeheartedly service based. Service teams think of their software as being a cog in a far larger machine. 

Be of the web, not behind the web.

your users weren't just customer ot businesspeople; they were other applications, and they really cared that your service was reliable. So applications became platforms, and building platforms is hard.

LinkedIn felt this pain as it evolved away from its original, monolithic Java app into 800-1,100 services. Complex dependenies led to instability, versioning issues caused painful lockstep relaeses, and early on, it wasn't clear that the new architecture was actually an improvement.

On difference in the way LinkedIn evolved it approach was its use of a messaging system built in-house: Kafka. Kafka added an asynchronous publish=subscribe model to the architecture that enabled trillions of messages a day to be transported around the organization.

