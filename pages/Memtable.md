tags:: [[Data Structure]]

- # Memtable
	- Memtable, short for "memory table," is a data structure used in computer science and database systems to temporarily store writes before they're committed to permanent storage like disk.
	- ## Memtables functionalities within a database system
		- **Temporary storage for writes**
			- When new data is written into a database, it's first inserted into the memtable, which resides in the system's memory (RAM). This enables fast write operations since memory access is much quicker than disk access.
		- **In-memory structure**
			- The memtable is often implemented as some variant of a data structure optimized for rapid inserts and lookups, like a hash table or a skip list. The structure is organized to facilitate quick retrieval and modification of data.
		- **Flush to disk**
			- As the memtable fills up or reaches a certain threshold, its contents are flushed to disk as a more permanent storage structure (like an SSTable in an LSM tree or a table in a traditional database). This process ensures durability, as data in memory can be volatile and lost during system failures.
		- **Fast read access**
			- Until the data is flushed to disk, the memtable serves as the primary source for read operations as well, allowing for quick access to recently written data.
		- **Concurrent use**
			- Database systems often allow concurrent writes to the memtable, ensuring multiple write operations can occur simultaneously without blocking each other.
	- The use of a memtable helps in optimizing write performance by taking advantage of the speed of memory while also ensuring data durability by periodically persisting it onto disk. It plays a crucial role in the functioning of databases, especially in scenarios where high write throughput and low latency are essential, by acting as a buffer between the incoming writes and the more permanent storage on disk.