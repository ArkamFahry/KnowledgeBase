tags:: [[DSA]], [[Data Structure]]

- # LSM-tree
	- LSM (Log-Structured Merge) tree is a data structure optimized for write-heavy workloads commonly used in databases and file systems. It's designed to efficiently handle a large volume of write operations while supporting read operations as well.
	- ## Components of an LSM tree
		- **[[Memtable]]**
			- This is an in-memory data structure where incoming writes are initially stored. It acts as a buffer for new data before it's flushed to disk.
		- **[[SSTable]] (Sorted String Tables)**
			- When the memtable reaches a certain size, it's flushed to disk as an immutable sorted table called an SSTable. These SSTables are sorted by keys to allow for efficient retrieval.
	- ## How data is written to a LSM-tree
		- **Incoming writes**
			- When data is written to the database, it's first added to the memtable in memory.
		- **Memtable flush**
			- Once the memtable reaches a certain size or threshold, it is written to disk as an SSTable. The new writes continue to go to the memtable.
		- **Compaction**
			- Over time, multiple SSTables may accumulate. Periodically, these SSTables are merged or compacted together to reduce the number of files and improve read efficiency. During compaction, duplicate keys are resolved, and the latest value for each key is retained.
	- ## How data is read to LSM-tree
		- When reading data, the LSM tree checks the memtable first for the most recent writes. If the data isn’t found in the memtable, it then searches the SSTables, starting with the most recent ones. This process ensures that the latest writes are quickly accessible.
	- ## Advantages of a LSM-tree
		- **Write optimization**
			- They excel in write-heavy workloads due to the sequential write nature of appending to the memtable and the periodic batched writes to SSTables.
		- **Space efficiency**
			- Compaction reduces the number of files and merges data, optimizing space utilization.
		- **Faster writes**
			- Writing to disk sequentially is generally faster than random writes, improving write performance.
	- ## Limitations of a LSM-tree
	- **Read amplification**
		- Reading involves checking both the memtable and multiple SSTables, which can lead to increased read latency compared to some other data structures.
	- **Compaction overhead**
		- The process of merging SSTables can be resource-intensive, impacting performance during compaction.
	- LSM trees are commonly used in various databases like [[Apache Cassandra]], [[LevelDB]], and [[RocksDB]] due to their ability to handle high-throughput write operations efficiently.