# OCC: Optimistic Concurrency Control
	- Optimistic Concurrency Control (OCC) is a method used in database management systems to handle concurrent access to data without locking. Unlike Pessimistic Concurrency Control, which assumes conflicts will occur and locks data to prevent conflicts, OCC assumes conflicts are unlikely and allows transactions to proceed without locking. Instead, OCC detects conflicts at the time of transaction commit and resolves them if they occur.
	- ## How Optimistic Concurrency Control works:
		- **Versioning**
			- In OCC, each data item is associated with a version number or timestamp that indicates the last time the item was read or modified. When a transaction reads a data item, it records the version number or timestamp of the item.
		- **Transaction Process**
			- **Read Phase**
				- When a transaction reads a data item, it records the version number or timestamp of the item.
			- **Write Phase**
				- When a transaction modifies a data item, it checks if the version number or timestamp of the item has changed since it was last read. If the version has not changed, the transaction proceeds with the update. If the version has changed, it indicates that another transaction has modified the item concurrently, and a conflict is detected.
		- **Conflict Detection and Resolution**
			- **Conflict Detection**
				- OCC detects conflicts at the time of transaction commit by comparing the version number or timestamp of each data item modified by the transaction with the current version of the item in the database. If any item's version has changed, a conflict is detected.
			- **Conflict Resolution**
				- When a conflict is detected, OCC typically aborts the transaction and notifies the application. The application can then decide how to resolve the conflict, such as by retrying the transaction or merging the changes.
		- **Transaction Commit**
			- If no conflicts are detected, the transaction is committed, and the updated data is written to the database. The version numbers or timestamps of the modified data items are incremented to indicate the changes.
		- **Performance Considerations**
			- OCC is well-suited for environments with low contention and a high degree of concurrency, as it eliminates the overhead of locking. However, it can lead to increased abort rates and retry attempts if conflicts occur frequently, which can impact performance.
	- In summary, Optimistic Concurrency Control is a concurrency control mechanism that allows transactions to proceed without locking and detects conflicts at the time of transaction commit. While it can improve performance in low-contention environments, it may lead to increased abort rates and retry attempts in high-contention scenarios.