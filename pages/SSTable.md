tags:: [[Data Structure]]

- # SSTable
	- SSTable (Sorted String Table) is a type of disk-based data structure used in many database systems to store data in a sorted manner for efficient retrieval. It's particularly associated with systems that use the LSM (Log-Structured Merge) tree for managing data.
	- ## Key characteristics of a SSTable
		- **Sorted storage**
			- Data within an SSTable is sorted by keys. This sorting allows for efficient lookup operations, making it easier to find specific data entries.
		- **Immutable structure**
			- Once an SSTable is written to disk, it remains unchanged. Any updates or modifications result in a new SSTable being created, which provides benefits in terms of data integrity and simplified read operations.
		- **Compression and compaction**
			- SSTables often incorporate techniques like compression to reduce disk space usage. Additionally, multiple SSTables may be merged or compacted periodically to optimize storage and enhance read performance by reducing the number of files to search.
		- **Sequential disk access**
			- The design of SSTables promotes sequential reads, which are generally faster on disk compared to random reads. This sequential access pattern contributes to improved read performance.
	- ## How SSTables are used
		- **Data storage**
			- When data is written to a database using [[LSM-tree]], it's first stored in a [[Memtable]] (in-memory buffer) and then periodically flushed to disk as an SSTable. These SSTables contain sorted, immutable data that forms a part of the database.
		- **Read operations**
			- When a read operation occurs, the database system checks these SSTables, starting from the most recent ones, to locate the required data. The sorted nature of SSTables allows for efficient searching, and the immutable structure simplifies read operations.
	- ## Advantages of SSTables
		- **Efficient read performance**
			- The sorted nature of SSTables and their sequential disk access patterns contribute to faster read operations, especially for range queries and lookups by key.
		- **Space efficiency**
			- Techniques like compression and compaction reduce disk space usage, optimizing storage.
	- ## Use cases for SSTables
		- SSTables are commonly used in various databases, including [[Apache Cassandra]], [[LevelDB]], and [[RocksDB]]. These databases leverage SSTables within the context of [[LSM-tree]] to efficiently manage and access large volumes of data, particularly in write-heavy workloads.
	- SSTables are fundamental in these systems for storing and organizing data on disk in a manner that facilitates both quick retrieval and efficient use of storage space.