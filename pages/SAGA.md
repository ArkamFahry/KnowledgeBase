# SAGA
	- SAGA refers to a design pattern used to manage distributed transactions within a microservices architecture. The term "SAGA" stands for "SAGAs or Cooperative Transactions."
	- A SAGA represents a sequence of local transactions, each updating data within a single service. These local transactions are coordinated in such a way that they maintain data consistency across multiple services in a distributed environment.
	- ## Types of SAGA's
		- **Choreography-based SAGA**
			- In this approach, each service involved in the transaction publishes events when it performs its local transaction. Other services listen to these events and trigger their respective local transactions accordingly.
		- **Orchestration-based SAGA**
			- Here, there's a central component (orchestrator) that coordinates the sequence of steps for the entire transaction. The orchestrator determines the order of local transactions and ensures the transaction's consistency.
	- SAGAs are essential in distributed systems where traditional ACID transactions are not feasible due to scalability and performance issues. They allow developers to maintain data consistency across multiple services despite the inherent complexity of distributed architectures.