tags:: [[Database]]

- # Distributed Database
	- A distributed database is a [[Database]] that is spread across multiple locations or nodes, where each node stores and manages a portion of the data. In contrast to a centralized database, where all data is stored in a single location, a distributed database distributes the data and processing tasks across a network of interconnected computers.
	- ## Key characteristics of distributed databases include
		- **Data Distribution**
			- The database is divided into partitions or fragments, and each fragment is stored on different nodes in the network. This distribution can be based on various factors, such as data ranges, hash values, or specific criteria.
		- **Autonomy**
			- Each node in a distributed database operates independently and has its own computing and storage resources. Nodes can function autonomously without relying on a central authority for all operations.
		- **Concurrency Control**
			- Distributed databases must manage multiple simultaneous transactions from different nodes. Concurrency control mechanisms ensure that transactions do not interfere with each other, maintaining the consistency of the data.
		- **Fault Tolerance**
			- Distributed databases often incorporate redundancy and fault-tolerant mechanisms to ensure system reliability. If one node fails, the system can continue to operate using other available nodes.
		- **Interconnectivity**
			- Nodes in a distributed database communicate with each other over a network, typically using protocols and communication channels. This allows them to share information and coordinate activities.
		- **Scalability**
			- Distributed databases can be more easily scaled by adding more nodes to the network, allowing for increased storage capacity, processing power, and improved performance as the demand for resources grows.
	- Distributed databases are commonly used in scenarios where large volumes of data need to be managed, and where geographical distribution or high availability requirements necessitate a decentralized approach to data storage and processing. They are employed in various applications, such as cloud computing, global enterprises, and online services.