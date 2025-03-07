- [[Event-Driven Architecture]]
- {{video https://www.youtube.com/watch?v=gOuAqRaDdHA}}
- Events are different from Messages ([[Message-Based Architecture]])
	- Events are raised after event has happened, not as a request
	- Producer is not reliant on consumer picking up the event
- Events are immutable
	- Messages are usually flushed from the queue after processing
- Mediated by an [[Event Broker]]
	- allows service to subscribe to event types they are interested in
- Useful to have different services that do not have hard time synch requirements
	- Batch processing/analytics
	- human-scale events
- Advantages
	- Decouples producer and consumers
	- New consumers can be added without changes to publisher
	- Dependency inversion
		- Both producer and consumer are dependent on a high-level abstraction, rather than low-level components
		- new implementations can replace old without issues
	- Scaling
		- Can spin up more subscribers to deal with load
- Disadvantages
	- Data Consistency
		- Delay between publishing and consumer picking the event up
			- Usually pretty small (milliseconds)
	- Duplicate messages
		- if a service goes offline, it will get messages since last checkpoint (from broker), which may include duplicates
		- Subscribers need to be idempotent
	- Complexity
		- more components and infrastructure to maintain