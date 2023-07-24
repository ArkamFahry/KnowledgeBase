- # Key Value Databases
	- ## What are Key-Value Databases
		- A Key-Value Database is a type of NoSQL (Not Only SQL) database that stores data in a simple key-value pair format. In this type of database, data is organized into collections of key-value pairs, where each key is unique and corresponds to a value, similar to how you might use a dictionary or a hash map in programming.
	- ## The basic structure of a key-value database is as follows
		- ```
		  Key1: Value1
		  Key2: Value2
		  Key3: Value3
		  ...
		  ```
	- ## Why are They useful
		- Key-value databases are known for their simplicity and scalability. They are often used in scenarios where fast and efficient access to data is crucial. The key-value model allows for rapid retrieval of data based on the keys, making it ideal for caching, session storage, user profiles, and other use cases where quick access is essential.
	- ## Some key features of key-value databases include
		- Schema-less
			- Unlike traditional relational databases, key-value databases are typically schema-less, meaning each item can have different attributes or fields without requiring a predefined schema.
		- Scalability
			- Key-value databases are designed to scale horizontally, allowing you to add more nodes to the cluster to accommodate increased data and traffic.
		- High Performance
			- Since data retrieval is based on keys, key-value databases can offer very high read and write throughput, making them suitable for use in high-performance applications.
		- No Complex Queries
			- Unlike SQL databases, key-value databases do not support complex queries that involve multiple tables or operations like joins. They focus on simple get, put, and delete operations based on keys.
		- Use Cases
			- Key-value databases are commonly used in various scenarios, including caching, real-time analytics, recommendation engines, gaming leaderboards, user sessions, and more.
	- ## Some Example for K/V Databases
		- Popular examples of key-value databases include [[Redis]], [[Memcached]] , [[Amazon DynamoDB]], [[Riak]], and [[Apache Cassandra]] (which is a hybrid between a key-value and a [[Columnar Databases]]). These databases are widely used in modern web applications and distributed systems to manage high-velocity data with low-latency access requirements.