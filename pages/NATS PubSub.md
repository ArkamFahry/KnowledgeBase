tags:: [[NATS]], [[PubSub]]

- # NATS PubSub
	- NATS PubSub is a messaging system that enables communication between different parts of a distributed system using the publish-subscribe messaging pattern. In this pattern, publishers send messages without specifying who the recipients (subscribers) are, and subscribers receive messages based on their interest in certain topics.
	- ## [[NATS]] PubSub workings in more detail
		- **Publishing Messages**
			- Publishers send messages to NATS without needing to know who or how many subscribers there are. Messages are sent to a specific subject, which acts as a category or topic for the message.
		- **Subscribing to Subjects**
			- Subscribers express interest in receiving messages from specific subjects. They create subscriptions to these subjects, and NATS delivers messages from those subjects to the subscribers.
		- **Message Delivery**
			- When a message is published to a subject, NATS delivers the message to all subscribers of that subject. This decoupling allows for a flexible and scalable messaging system where publishers and subscribers are loosely connected.
	- Overall, NATS PubSub is a lightweight, high-performance messaging system that provides a simple and efficient way to build distributed systems and handle real-time communication between components.
	- ## NATS PubSub Resources
		- [Publish-Subscribe - NATS Docs](https://docs.nats.io/nats-concepts/core-nats/pubsub)