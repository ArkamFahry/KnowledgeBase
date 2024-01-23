tags:: [[Software Design Pattern]]

- # Behavioral Pattern
	- Behavioral patterns in software design refer to patterns that focus on how objects and classes interact and communicate with each other. These patterns are concerned with the assignment of responsibilities between objects, defining how they communicate, and managing their behaviors.
	- ## Behavioral design patterns include
		- **Observer Pattern**
			- This pattern establishes a one-to-many dependency between objects, so that when one object changes state, all its dependents are notified and updated automatically.
		- **Strategy Pattern**
			- It defines a family of algorithms, encapsulates each one of them, and makes them interchangeable. This pattern allows the algorithm to vary independently from the clients that use it.
		- **Command Pattern**
			- It encapsulates a request as an object, thereby allowing parameterization of clients with queues, requests, and operations. This pattern also supports the operations to be performed in a sequence, undoable, or logged.
		- **Iterator Pattern**
			- This pattern provides a way to access elements of an aggregate object sequentially without exposing its underlying representation. It abstracts the traversal through a collection of objects.
		- **Chain of Responsibility Pattern**
			- It allows an object to pass a request along a chain of potential handlers until one of them handles the request. This pattern decouples senders and receivers of requests.
		- **State Pattern**
			- This pattern allows an object to alter its behavior when its internal state changes. It appears as if the object has changed its class.
		- **Template Method Pattern**
			- It defines the skeleton of an algorithm in the superclass but lets subclasses override specific steps of the algorithm without changing its structure.
		- **Interpreter Pattern**
			- This pattern defines a grammatical representation for a language and an interpreter to interpret sentences in that language.
	- Each of these patterns addresses specific aspects of interaction and behavior between objects in software systems, promoting flexibility, reusability, and maintainability in the codebase.