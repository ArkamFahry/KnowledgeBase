tags:: [[PostgreSQL]]

- # PostgreSQL SKIP LOCKED
	- PostgreSQL, the `SKIP LOCKED` clause is used in the context of the `SELECT ... FOR UPDATE` statement. This clause allows a query to skip rows that are already locked by other transactions, rather than waiting for those locks to be released.
		- ## Brief explanation of `SKIP LOCKED`
		- **SELECT ... FOR UPDATE**
			- The `SELECT ... FOR UPDATE` statement is used to lock rows in a table temporarily, preventing other transactions from modifying or locking those rows until the current transaction is committed.
		- **SKIP LOCKED**
			- The `SKIP LOCKED` clause is an extension in PostgreSQL that modifies the behavior of the `FOR UPDATE` clause. When you include `SKIP LOCKED` in your `SELECT ... FOR UPDATE` statement, it instructs the database to skip rows that are already locked by other transactions rather than waiting for those locks to be released.
		- **Example**
			- ```sql
			  SELECT * FROM your_table FOR UPDATE SKIP LOCKED;
			  ```
				- In this example, the query selects rows from `your_table` and applies the `FOR UPDATE` lock, but it skips any rows that are already locked by other transactions.
		- **Use Case**
			- This feature is particularly useful in scenarios where you want to process or update rows in parallel by multiple transactions without waiting for locks held by other transactions. It helps in reducing contention and improving overall performance.
	- It's important to note that the `SKIP LOCKED` functionality is beneficial in certain scenarios but might not be suitable for all use cases. It depends on the specific requirements of your application and the nature of the transactions you are handling. Additionally, the behavior and syntax of database systems may vary, so it's essential to refer to the documentation of the specific PostgreSQL version you are using for the most accurate and up-to-date information.