tags:: [[Software Design Pattern]]

- # Creational Pattern
	- Creational design patterns in software engineering focus on object creation mechanisms, providing ways to create objects while hiding the creation logic, making the system more flexible and decoupled from the specific classes it needs to instantiate. These patterns deal with object creation mechanisms, trying to create objects in a manner suitable to the situation.
	- ## Creational design patterns include
		- **Singleton Pattern**
			- This pattern ensures that a class has only one instance and provides a global point of access to it. It's useful when exactly one object is needed to coordinate actions across the system.
		- **Factory Method Pattern**
			- It defines an interface for creating an object, but allows subclasses to alter the type of objects that will be created. It provides a way for a class to delegate the instantiation to subclasses.
		- **Abstract Factory Pattern**
			- This pattern provides an interface for creating families of related or dependent objects without specifying their concrete classes. It's useful when a system needs to be independent of how its objects are created, composed, and represented.
		- **Builder Pattern**
			- It separates the construction of a complex object from its representation, allowing the same construction process to create different representations. It's useful when there is a need to create an object with many optional parameters.
		- **Prototype Pattern**
			- It creates new objects by copying an existing object, known as the prototype. This pattern is useful when the cost of creating an object is more expensive or complex than copying an existing object.
		- **Object Pool Pattern**
			- It creates a set of objects (a pool) that can be reused rather than creating and destroying them on demand. This pattern is beneficial when creating and destroying objects is resource-intensive.
	- Each of these creational patterns addresses various scenarios related to object creation, instantiation, and the way instances of classes are created, promoting flexibility, scalability, and maintainability in software design.