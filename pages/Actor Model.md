# Actor Model
	- The [Actor Model](https://en.wikipedia.org/wiki/Actor_model) is a conceptual framework for building concurrent and distributed systems. It was first proposed by [Carl Hewitt](https://en.wikipedia.org/wiki/Carl_Hewitt) in the 1970s as a way to model concurrent computation. The key idea behind the Actor Model is to treat actors as the fundamental unit of computation, where each actor is an independent entity that can communicate with other actors by sending and receiving messages.
	- ## The key concepts of the Actor Model
		- **Actor**
			- An actor is a computational entity that encapsulates state, behavior, and a mailbox for receiving messages. Actors are independent of each other and can only communicate by exchanging messages. Actors can create new actors, send messages to other actors, and change their own behavior in response to messages.
		- **Message**
			- Messages are the means by which actors communicate with each other. Messages are asynchronous, meaning that an actor can continue its computation without waiting for a response after sending a message. Messages can contain data or instructions for the receiving actor.
		- **Address**
			- Each actor has a unique address, which is used by other actors to send messages to it. Addresses are used to identify and communicate with specific actors.
		- **Mailbox**
			- Each actor has a mailbox, which is a queue that stores incoming messages. When an actor receives a message, it is placed in its mailbox and can be processed by the actor in the order they were received.
		- **Behavior**
			- An actor's behavior defines how it will react to messages it receives. Actors can change their behavior in response to messages or external events. This allows actors to dynamically adapt to changing conditions.
		- **Concurrency**
			- The Actor Model is inherently concurrent, meaning that multiple actors can execute concurrently. Actors can be executed on different threads or even different machines, allowing for distributed computing.
		- **Fault tolerance**
			- The Actor Model provides built-in fault tolerance mechanisms. Since actors are isolated from each other, failures in one actor do not affect other actors. Actors can also be supervised, allowing for automatic recovery from failures.
		- **Scalability**
			- The Actor Model is highly scalable, as actors can be distributed across multiple machines. This allows for the creation of large-scale systems that can handle a high volume of concurrent operations.
	- Overall, the Actor Model provides a powerful and flexible framework for building concurrent and distributed systems. By treating actors as independent entities that communicate through messages, the Actor Model simplifies the design of complex systems and provides a solid foundation for building reliable and scalable applications.