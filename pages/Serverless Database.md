tags:: [[Serverless]]

- # Serverless Database
	- Serverless databases, sometimes referred to as serverless database services or serverless data storage, follow a similar principle to serverless computing. They aim to abstract the management of databases, scaling, and infrastructure away from developers.
	- These databases are designed to handle data storage and retrieval without the need for users to provision, manage, or scale the underlying infrastructure.
	- ## Overview of serverless databases
		- **Automatic Scaling:** Serverless databases automatically handle scaling based on the workload and demand. As the data grows or as more resources are required, these databases adjust their capacity without requiring manual intervention.
		- **Pay-Per-Use Model:** Similar to serverless computing, serverless databases often operate on a pay-as-you-go or pay-per-use pricing model. Users are charged for the resources consumed rather than pre-provisioned capacity.
		- **Managed Infrastructure:** With serverless databases, the cloud provider manages the infrastructure, including server provisioning, software patching, backups, and other maintenance tasks. Users can focus on using the database rather than managing its underlying infrastructure.
		- **Automatic Replication and High Availability:** Many serverless database services offer built-in features for data replication and high availability, ensuring data durability and accessibility even in the event of hardware failures.
		- **Scalable Performance:** These databases are designed to provide consistent performance even as workloads fluctuate. They can automatically adjust resources to handle varying levels of traffic without affecting performance.
		- **Support for Various Data Models:** Serverless databases often support different data models like relational (SQL), NoSQL, document-oriented, key-value stores, etc., catering to different application needs.
		- **Ease of Use and Integration:** They usually come with easy-to-use interfaces, APIs, and integration capabilities, enabling developers to seamlessly incorporate the database service into their applications.
	- Popular serverless database offerings include [[Amazon Aurora Serverless]], [[Azure Cosmos DB]] , [[Firestore]], [[PlanetScale]], [[Neon]] and others. These services provide a range of functionalities, allowing developers to build scalable applications without worrying about the intricacies of managing the database infrastructure.
	- Overall, serverless databases aim to simplify data management, reduce operational overhead, and provide a cost-effective solution for storing and accessing data in modern applications.