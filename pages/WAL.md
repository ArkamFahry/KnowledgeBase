# WAL
	- The Write-Ahead Logging (WAL) technique is a method used by database systems to ensure durability, consistency, and performance in managing transactions and handling data modifications.
	- ## WAL mechanism have two main components
		- **Log**
			- A separate file called the WAL log file, which records changes to the database in a sequential manner. It contains a record of all modifications made to the database, including inserts, updates, and deletes.
		- **Data Pages**
			- The actual database files that store the data.
	- ## How a WAL works
		- **Logging Changes**
			- When a transaction modifies data in the database, these changes are first written to the WAL log file before they're applied to the actual data pages. This means that before the changes are made to the database files, they are first recorded in the log.
		- **Committing Transactions**
			- Once a transaction is completed and ready to be committed, the database system writes a commit record into the log. This indicates that the changes recorded in the log can now be applied to the data pages.
		- **Durability and Crash Recovery**
			- Because the log records changes before applying them to the data pages, in case of a system crash or failure, the database system can use the WAL log to recover the committed transactions that may not have been written to the data pages before the crash. During recovery, the system replays the log, reapplying the changes to bring the database back to a consistent state.
	- ## Benefits of WAL:
		- **Durability**
			- It ensures that committed transactions are saved and recoverable, even in the event of a system failure.
		- **Performance**
			- Writing to a sequential log file is often faster than making random writes to the database's data pages, enhancing overall system performance.
		- **Concurrency**
			- It allows multiple transactions to write changes concurrently to the log, improving the database's ability to handle multiple transactions simultaneously.
	- WAL is a widely used technique in many relational and non-relational database systems, providing a reliable and efficient way to manage data modifications while ensuring data integrity and crash recovery capabilities.