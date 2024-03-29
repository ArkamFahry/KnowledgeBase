tags:: [[CDC]]

- # Debezium
	- ![debezium.png](../assets/debezium_1703582472679_0.png)
	- Debezium is an open-source distributed platform for change data capture (CDC) that captures and streams database changes in real-time. It's designed to monitor database changes, extract them, and then push these changes to various downstream systems or applications. It supports a wide range of databases, including MySQL, PostgreSQL, SQL Server, MongoDB, and others.
	- ## Components and features of Debezium
		- **Connectors**
			- Debezium provides connectors tailored for different databases. These connectors monitor the database's transaction log to capture changes (inserts, updates, deletes), converting them into a stream of events in a specific format (like Apache Kafka's Connect framework).
		- **Apache Kafka Integration**
			- Debezium works seamlessly with [[Apache Kafka]], a distributed streaming platform. It uses Kafka's distributed architecture to ensure scalability, fault tolerance, and efficient message passing. Debezium writes database changes as Kafka messages, allowing easy integration with downstream applications.
		- **Event-Driven Architecture**
			- It follows an event-driven architecture, where each database operation is captured as an event. This makes it suitable for building real-time streaming applications, microservices architectures, and enabling event sourcing patterns.
		- **Schema Changes**
			- Debezium tracks and captures database schema changes, allowing downstream applications to stay updated with any alterations made to the database structure.
		- **Reliable and Fault-Tolerant**
			- Debezium is designed for reliability and fault tolerance. It ensures that even if there are failures or interruptions, it can resume capturing changes from the point of interruption without losing data.
		- **Integration with Various Ecosystems**
			- It integrates well with other tools and frameworks within the Kafka ecosystem, allowing for easy consumption of data by applications, analytics platforms, or storage systems.
		- **Community Support**
			- Debezium benefits from an active open-source community that contributes to its development, supports users, and continuously improves its functionality and compatibility with different databases.
	- ## Example Debezium Config
		- ```json
		  {
		      "connector.class": "io.debezium.connector.postgresql.PostgresConnector",
		      "database.dbname": "neondb",
		      "database.hostname": "ep-wispy-glitter-a5zg2715.us-east-2.aws.neon.tech",
		      "database.password": "7JbCwzMf5scd",
		      "database.port": "5432",
		      "database.server.name": "neon",
		      "database.user": "ArkamFahry",
		      "key.converter": "org.apache.kafka.connect.json.JsonConverter",
		      "key.converter.schemas.enable": true,
		      "plugin.name": "pgoutput",
		      "publication.autocreate.mode": "filtered",
		      "publication.name": "cdc_publication",
		      "schema.include.list": "public",
		      "value.converter": "org.apache.kafka.connect.json.JsonConverter",
		      "value.converter.schemas.enable": true
		  }
		  ```
	- By leveraging Debezium, developers can build scalable, event-driven architectures that react to changes in databases in real-time. It's particularly useful in scenarios where applications need immediate access to updated database information without putting extra load on the database itself.
	- ## Debezium Resources
		- [Debezium](https://debezium.io/)
		- [GitHub - debezium/debezium: Change data capture for a variety of databases. Please log issues at https://issues.redhat.com/browse/DBZ.](https://github.com/debezium/debezium)