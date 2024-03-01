tags:: [[Replication]]

- # Logical Replication
	- Logical Replication refers to the process of replicating data changes at the logical level, typically by replicating the changes made to database objects (such as tables, views, or schemas) rather than replicating the physical data blocks themselves.
	- This form of replication is often used in database systems to replicate data between different databases or database instances. Unlike physical replication, which replicates the exact bytes of data blocks, logical replication replicates the changes in a way that is independent of the underlying storage format.
		- ## Advantages of Logical Replication
			- **Flexibility**
				- It allows replication between databases with different schemas or versions, as long as the logical structure of the data remains compatible.
			- **Selective Replication**
				- It allows replicating only specific tables or data subsets, providing more granular control over what data is replicated.
			- **Lower Impact**
				- Since it operates at a higher level of abstraction, it can be less resource-intensive compared to physical replication, especially for large databases.
			- Easier Maintenance**
				- Logical replication can be easier to manage and maintain, as it is often more straightforward to set up and configure compared to physical replication.
	- [[PostgreSQL]], for example, offers logical replication as a feature that allows you to replicate changes made to a database to one or more other databases, enabling you to build scalable and fault-tolerant systems.