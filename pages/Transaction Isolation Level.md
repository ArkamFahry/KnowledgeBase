tags:: [[Transaction]]

- # Transaction Isolation Level
	- Transaction isolation level defines the degree to which transactions are isolated from each other in a database system. Different isolation levels provide different trade-offs between consistency, concurrency, and performance.
	- ## The standard isolation levels
		- **Read Uncommitted**
			- This is the lowest isolation level. It allows transactions to read data that has been modified but not yet committed by other transactions. It can lead to dirty reads, non-repeatable reads, and phantom reads.
		- **Read Committed**
			- This isolation level ensures that a transaction can only read data that has been committed by other transactions. It prevents dirty reads but allows non-repeatable reads and phantom reads.
		- **Repeatable Read**
			- This isolation level ensures that if a transaction reads a set of rows multiple times, it will see the same data each time. It prevents dirty reads and non-repeatable reads but allows phantom reads.
		- **[[Serializable Transaction]]**
			- This is the highest isolation level. It ensures that transactions are executed as if they were the only transactions running in the system. It prevents dirty reads, non-repeatable reads, and phantom reads but can lead to reduced concurrency and performance.
		- **Snapshot Isolation**
			- This isolation level provides a consistent snapshot of the database at the beginning of each transaction. It allows transactions to read data without blocking other transactions, providing a high level of concurrency. However, it can lead to some anomalies, such as write skew.
	- Each isolation level provides a different balance between consistency, concurrency, and performance. The choice of isolation level depends on the requirements of the application and the desired trade-offs.