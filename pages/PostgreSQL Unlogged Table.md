tags:: [[PostgreSQL]]

- # PostgreSQL Unlogged Table
	- Sure, in PostgreSQL, tables can be created as "unlogged". An unlogged table in PostgreSQL is a table that doesn't write any [[WAL]] (Write-Ahead Logging) information. This means that it doesn't record its changes in the transaction log, which can make it faster because it reduces the overhead of maintaining the log.
	- However, this speed gain comes with a trade-off of durability. Unlogged tables are not crash-safe. If there is a crash or a server failure, the data in an unlogged table might be lost, as it doesn't have the same level of protection as a regular table that writes to the WAL.
	- Unlogged tables are useful for temporary or transient data that can be easily reconstructed or is not critical in case of loss. For example, intermediate data in complex calculations or session-specific temporary data might be good candidates for unlogged tables.
	- To create an unlogged table in PostgreSQL, you can use the `UNLOGGED` option
		- ```sql
		  CREATE UNLOGGED TABLE table_name (
		    column1 datatype,
		    column2 datatype,
		    ...
		  );
		  ```
	- And to convert an existing table to unlogged
		- ```sql
		  ALTER TABLE table_name SET UNLOGGED;
		  ```
	- Remember, using unlogged tables should be a conscious decision based on the specific requirements of your application, weighing the performance benefits against the risk of potential data loss in case of a system failure.