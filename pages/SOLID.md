tags:: [[Software Architecture]]

- # SOLID: An acronym that represents a set of five design principles to make software designs more understandable, flexible, and maintainable
	- ## SOLID is split into five core principals
		- ### S : Single Responsibility Principle (SRP)
			- A class should have only one reason to change. In other words, it should have only one job or responsibility within the software system.
		- ### O : Open/Closed Principle (OCP)
			- Software entities (classes, modules, functions, etc.) should be open for extension but closed for modification. This means that you can add new functionality without altering existing code.
		- ### L : Liskov Substitution Principle (LSP)
			- Objects of a superclass should be replaceable with objects of its subclasses without affecting the correctness of the program. Subtypes must be substitutable for their base types without changing the desired properties of the program.
		- ### I : Interface Segregation Principle (ISP)
			- Many specific interfaces are better than one general interface. It suggests that a class should not be forced to implement interfaces it doesn't use. Instead, it should have specific interfaces tailored to its needs.
		- ### D : Dependency Inversion Principle (DIP)
			- High-level modules/classes should not depend on low-level modules/classes directly; they should depend on abstractions. Abstractions should not depend on details; details should depend on abstractions. This principle promotes loose coupling between software modules.