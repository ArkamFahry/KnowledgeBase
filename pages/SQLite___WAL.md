- # SQLite WAL: SQLite Write-Ahead Logging
  id:: 64998001-0aeb-458e-a5fc-d2d3dc7ae5d2
  title:: SQLite/WAL
	- ## What is WAL
	  id:: 64998134-b26a-4380-b9ef-d4cb44f8bb63
		- SQLite WAL mode stands for Write-Ahead Logging mode. It is a journaling mode in SQLite that improves the concurrency and performance of database operations. In WAL mode, SQLite writes transactions to a separate log file, known as the write-ahead log (WAL), instead of modifying the original database file directly. Then the transactions that are appended in the WAL file are sent back into the original database
	- ## Checkpointing
		- The process of appending the WAL file back into the original database. Moving the WAL file transactions back into the database is called a "*checkpoint*".
		- Another way to think about the difference between rollback and write-ahead log is that in the rollback-journal approach, there are two primitive operations, reading and writing, whereas with a write-ahead log there are now three primitive operations: reading, writing, and checkpointing.
		- By default, SQLite does a checkpoint automatically when the WAL file reaches a threshold size of 1000 pages. The SQLITE_DEFAULT_WAL_AUTOCHECKPOINT compile-time option can be used to specify a different default.) Applications using WAL do not have to do anything in order to for these checkpoints to occur. But if they want to, applications can adjust the automatic checkpoint threshold. Or they can turn off the automatic checkpoints and run checkpoints during idle moments or in a separate thread or process.
	- ## Concurrency
		- In WAL-mode databases, during a read operation, the database remembers the location of the last valid commit record in the Write-Ahead Log (WAL). This location is called the "end mark." Each reader can have its own end mark, which remains unchanged throughout the transaction, ensuring that a reader sees the database content as it existed at a specific point in time.
		- When a reader needs a page of content, it checks the WAL for the page. If a copy of the page exists in the WAL before the reader's end mark, it retrieves the last copy from the WAL. Otherwise, it reads the page from the original database file. To improve performance, a data structure called the "wal-index" is maintained in shared memory, allowing readers to locate pages in the WAL quickly.
		- Writers append new content to the end of the WAL file without interfering with readers. However, there can only be one writer at a time since there is only one WAL file. Writers and readers can operate concurrently.
		- A checkpoint operation transfers content from the WAL back into the original database file. Checkpoints can run concurrently with readers but must stop when reaching a page in the WAL beyond any current reader's end mark. This ensures that the checkpoint does not overwrite parts of the database file actively used by readers. The checkpoint resumes from where it left off in the next invocation.
		- If the entire WAL has been transferred to the database, synced, and no readers are using the WAL, a writer will rewind the WAL to the beginning and start adding new transactions there. This prevents the WAL file from growing indefinitely.
		- In summary, the WAL-mode in databases allows concurrent read and write operations by maintaining a log of changes. Readers use the WAL and the original database file to access data, while writers append new content to the WAL. Checkpoints transfer data from the WAL back to the database file. Shared memory and the wal-index structure improve performance.
	- ## Performance Considerations
		- The Write-Ahead Log (WAL) is a mechanism used in database systems to ensure data integrity and improve performance. When a write transaction occurs, the content is written to the WAL file, which allows for faster writes since it only involves writing the content once. However, this sacrifices durability in case of power loss or system reboot.
		- On the other hand, read performance can be affected as the WAL file grows larger because each reader needs to check the WAL file for content, and the time required for this check increases with the size of the file. The wal-index helps improve this process, but performance still decreases with a larger WAL file. To maintain good read performance, it's important to keep the WAL file size small by regularly performing checkpoints.
		- Checkpointing involves syncing the WAL to persistent storage before moving its content into the database. It also requires syncing the database file before resetting the WAL. Checkpoints are slower than write transactions because they involve more seeking operations and syncing operations to ensure data durability.
		- The default strategy is to let write transactions grow the WAL until it reaches around 1000 pages, and then run a checkpoint for each subsequent write transaction until the WAL size is reduced. This approach allows most write transactions to be fast, but occasional write transactions triggering a checkpoint can be slower. If this behavior is undesirable, the application can disable automatic checkpointing and run checkpoints separately.
		- It's important to note that the frequency of checkpoints affects the tradeoff between read and write performance. Running frequent checkpoints improves read performance but may reduce write performance. Choosing the right checkpoint strategy depends on the specific requirements of the application. By default, running a checkpoint once the WAL reaches 1000 pages works well in test applications, but different strategies may be more effective for other platforms or workloads.
	- ## Advantages of SQLite WAL Mode
		- Improved Write Performance
			- In WAL mode, SQLite writes database changes to a separate log file instead of modifying the original database file directly. This allows concurrent writes to occur without blocking other readers or writers, resulting in improved write performance. Only checkpoint operations synchronize the log file with the database file.
		- Reduced Disk I/O
			- Since SQLite writes changes to the separate log file, the database file itself is not modified during most write operations. This reduces disk I/O as only the log file needs to be updated, resulting in faster write operations and improved overall performance.
		- Better Concurrency
			- In WAL mode, multiple connections can read from the database file concurrently, while still allowing a single connection to perform write operations. This enables higher concurrency, as readers are not blocked by writers, and multiple readers can access the database simultaneously.
		- Crash Recovery
			- The WAL mode provides better crash recovery compared to other journaling modes in SQLite. In the event of a crash or power failure, SQLite can use the log file to replay the changes and bring the database back to a consistent state. This reduces the likelihood of database corruption and makes recovery faster and more reliable.
		- Improved Database Safety
			- WAL mode provides better durability and atomicity guarantees compared to other journaling modes. The log file ensures that changes are written in a sequential and consistent manner, preserving the integrity of the database even in the event of unexpected interruptions.
		- Reduced Database Fragmentation
			- With WAL mode, the database file remains largely unchanged during write operations, leading to reduced fragmentation. This can help maintain efficient disk usage and prevent performance degradation due to excessive file fragmentation.
	- ## How to setup WAL Mode
		- By default, an SQLite database connection uses the journaling mode "DELETE". To convert it to the Write-Ahead Logging (WAL) mode, you can execute the following pragma command:
			- id:: 64998a49-e196-4d4d-9ab4-03633d976b13
			  ```sql
			  PRAGMA journal_mode=WAL;
			  ```
		- If the conversion to WAL mode is successful, the pragma command will return the string "wal". However, if the conversion cannot be completed due to certain limitations in the underlying system, the journaling mode will remain unchanged, and the returned string will represent the previous journaling mode (e.g., "delete").
		- If needed WAL mode can be activated using the SQLite Connection string and appending **journal_mode=WAL** to the end like shown below
			- ```sql
			  sqlite3 mydatabase.db?journal_mode=WAL
			  ```
		- ### WAL with Extra Configuration
			- Checkpointing Frequency
				- By default, SQLite automatically checkpoints the WAL file to merge changes into the main database file periodically. You can adjust the checkpointing frequency using the `wal_autocheckpoint` pragma.
					- ```sql
					   PRAGMA wal_autocheckpoint = 1000;
					   ```
				- This sets the checkpoint to occur after approximately 1000 database page changes. Adjusting this value can impact the balance between write performance and checkpointing frequency.
			- Synchronous Mode
				- SQLite offers different synchronous modes that control how data is written to disk. In WAL mode, the `synchronous` pragma can be set to control the disk synchronization behaviour.
					- ```sql
					   PRAGMA synchronous = NORMAL;
					   ```
				- This sets the synchronous mode to `NORMAL`, where SQLite syncs the database file to disk at critical moments but allows the operating system to control the timing of the actual disk writes. You can choose from different modes like `OFF`, `NORMAL`, `FULL`, or `EXTRA` based on your durability requirements.
			- WAL Journal Size
				- The size of the WAL file can impact performance and disk space usage. The `wal_pages` pragma allows you to set the maximum size of the WAL file in database pages. For example:
					- ```sql
					   PRAGMA wal_pages = 4096;
					   ```
				- This sets the maximum size of the WAL file to approximately 4 MB (assuming a database page size of 1024 bytes). Adjusting this value can influence the frequency of checkpointing and the disk space requirements for the WAL file.
			- Journal Size Limit
				- In addition to the WAL file size, you can also set a limit on the size of the rollback journal file (used for compatibility purposes). The `journal_size_limit` pragma allows you to specify the maximum size of the rollback journal file in bytes. For example:
					- ```sql
					   PRAGMA journal_size_limit = 1048576;
					   ```
				- This sets the maximum size of the rollback journal file to approximately 1 MB. Adjusting this value can affect the amount of disk space used by the rollback journal.