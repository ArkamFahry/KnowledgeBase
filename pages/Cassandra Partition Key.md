tags:: [[Apache Cassandra]], [[ScyllaDB]]

- # Cassandra Partition Key
- A Cassandra partition key plays a pivotal role in data distribution across the nodes in a cluster. Designing an efficient partition key involves considering several key characteristics to ensure optimal performance and scalability.
- ## Characteristics of a Good Cassandra Partition Key
	- **Cardinality**
		- High cardinality ensures even data distribution across nodes. Using a column with unique or diverse values helps avoid hotspots.
			- In a table storing user data, using a unique user ID as the partition key distributes data evenly among nodes, preventing a single node from bearing a disproportionate load.
			- ```cql
			  CREATE TABLE users (
			      user_id UUID PRIMARY KEY, -- High cardinality UUID as the partition key
			      username TEXT,
			      email TEXT,
			      age INT
			  );
			  ```
			- Using a UUID as the partition key ensures high cardinality, distributing user data across nodes evenly. This prevents hotspots as each user ID is unique.
	- **Query Distribution**
		- Align the partition key with common query patterns to evenly distribute queries across nodes. This helps in leveraging parallelism for faster queries.
			- If your application frequently retrieves data based on geographical regions, using a country code or region as a partition key can distribute queries related to different regions across nodes.
			- ```cql
			  CREATE TABLE sensor_data (
			      sensor_id UUID,
			      timestamp TIMESTAMP,
			      value DOUBLE,
			      PRIMARY KEY (sensor_id, timestamp) -- Composite partition key
			  );
			  ```
			- In this example, the composite partition key `(sensor_id, timestamp)` distributes sensor data across nodes. Queries for specific sensors within certain time ranges distribute workload across nodes efficiently.
	- **Data Access Patterns**
		- Consider how your application accesses data. The partition key should reflect the way data is commonly accessed to optimize retrieval.
			- For a time series data store, using timestamps as a partition key allows efficient retrieval of data within a specific time range.
			- ```cql
			  CREATE TABLE purchases_by_category (
			      category TEXT,
			      purchase_id UUID,
			      purchase_details TEXT,
			      PRIMARY KEY (category, purchase_id) -- Category-based partition key
			  );
			  ```
			- Here, the partition key is based on the purchase category. Accessing purchases by category aligns with common query patterns, ensuring efficient data retrieval for specific categories.
	- **Size**
		- Smaller partition keys are generally more efficient as they reduce overhead. However, avoid excessively large partition keys that may lead to performance issues.
			- Using a hash or a portion of a UUID as a partition key rather than the entire UUID can reduce the key size while maintaining uniqueness.
			- ```cql
			  CREATE TABLE logs (
			      log_id UUID,
			      log_time TIMESTAMP,
			      log_info TEXT,
			      PRIMARY KEY (log_id) -- Partial UUID as the partition key
			  );
			  ```
			- Using a partial UUID as the partition key reduces its size while maintaining uniqueness. This optimizes storage and retrieval performance.
	- **Distribution Balance**
		- Aim for an even distribution of data across nodes to prevent uneven resource utilization or hotspots.
			- If dealing with product data, selecting a well-distributed attribute such as category or SKU as the partition key helps evenly distribute products across nodes.
			- ```cql
			  CREATE TABLE products (
			      sku TEXT PRIMARY KEY, -- Well-distributed SKU as the partition key
			      name TEXT,
			      price DECIMAL,
			      category TEXT
			  );
			  ```
			- Choosing a well-distributed attribute like SKU ensures products are evenly distributed across nodes, preventing overload on any specific node.
	- **Immutability**
		- Ideally, the partition key should be immutable. Changing the partition key values should be avoided as it triggers data movement during reassignment.
			- Using a user's email as a partition key is preferable over using a mutable attribute like username, which users might change.
			- ```cql
			  CREATE TABLE sensor_readings (
			      sensor_id UUID,
			      reading_time TIMESTAMP,
			      reading_value DOUBLE,
			      PRIMARY KEY (sensor_id, reading_time) -- Immutable sensor_id as the partition key
			  );
			  ```
			- Using an immutable attribute like `sensor_id` as the partition key ensures stability, avoiding data redistribution caused by updates to the partition key values.
	- When designing a partition key, it's crucial to analyze the application's specific requirements, anticipated data growth, and access patterns. A well-chosen partition key can significantly enhance Cassandra's performance and scalability by distributing data efficiently across the cluster.