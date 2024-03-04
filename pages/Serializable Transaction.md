tags:: [[Transaction]], [[Transaction Isolation Level]]

- # Serializable Transaction
	- A Serializable Transaction is the highest isolation level in database transactions, ensuring that transactions are executed as if they were the only transactions running in the system. This means that the outcome of running transactions concurrently is the same as if they were executed sequentially, one after the other.
	- To achieve serializability, a database management system (DBMS) uses various concurrency control mechanisms, such as locking and multi-version concurrency control ([[MVCC]]) or deterministic optimistic concurrency control ([[DOCC]]).
	- ## How a Serializable Transaction typically works
		- **Concurrency Control**
			- The DBMS ensures that multiple transactions can execute concurrently without interfering with each other. This is achieved through locking mechanisms, where transactions acquire locks on data items to prevent other transactions from accessing or modifying them concurrently.
		- **Conflict Detection**
			- The DBMS detects conflicts between transactions that could lead to incorrect results if not handled properly. These conflicts include read-write conflicts (one transaction reads data while another writes to it) and write-write conflicts (two transactions write to the same data item).
		- **Locking**
			- Serializable Transactions often use strict two-phase locking to ensure serializability. In the first phase (growing phase), a transaction acquires all the locks it needs before performing any modifications. In the second phase (shrinking phase), the transaction releases all its locks.
		- **Isolation**
			- Serializable Transactions provide a high level of isolation, ensuring that the intermediate state of a transaction is not visible to other transactions until it commits. This prevents dirty reads, non-repeatable reads, and phantom reads.
		- **Transaction Management**
			- Transactions are managed by the DBMS, which ensures that they are executed atomically (all or nothing), consistently (preserving the database in a valid state), and durably (changes are permanent).
		- **Transaction Serialization**
			- Transactions are executed in a serial order, even if they are actually executed concurrently. This ensures that the final result of executing transactions is the same as if they were executed one after the other.
	- Serializable Transactions are essential for maintaining data integrity and consistency in database systems, especially in systems where concurrent access to data is common. However, they can also lead to reduced concurrency and performance compared to lower isolation levels, as transactions may need to wait for locks to be released.