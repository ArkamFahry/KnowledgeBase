# SQL: Structured Query Language
	- SQL stands for Structured Query Language. It's a specialized programming language designed for managing and manipulating relational databases. It allows users to interact with databases by performing tasks like querying data, updating and modifying data, defining and altering database structures, and managing permissions.
	- ## Core functions of SQL can be broken down into several categories
		- **Data Querying**
			- SQL enables users to retrieve specific information from a database using commands like SELECT, which allows you to specify columns, tables, conditions, and sorting criteria to filter and retrieve data.
				- ```sql
				  SELECT column1, column2 FROM table_name WHERE condition;
				  ```
		- **Data Manipulation**
			- SQL facilitates the modification of database records through commands like INSERT, UPDATE, and DELETE. These commands add new data, modify existing data, or remove data from a table, respectively.
				- ```sql
				  INSERT INTO table_name (column1, column2) VALUES (value1, value2);
				  ```
		- **Data Definition**
			- SQL allows the creation, alteration, and deletion of database structures like tables, indexes, views, and schemas using commands like CREATE, ALTER, and DROP.
				- ```sql
				  CREATE TABLE table_name (
				    column1 datatype,
				    column2 datatype,
				    ...
				  );
				  ```
		- **Data Control**
			- SQL manages access to the database by granting or revoking permissions to users and roles using commands like GRANT and REVOKE.
				- ```sql
				  GRANT SELECT ON table_name TO user_name;
				  ```
	- SQL is used by various relational database management systems (RDBMS) like [[MySQL]], [[PostgreSQL]], Oracle, SQL Server, and [[SQLite]]. While the syntax may differ slightly among these systems, the fundamental SQL commands and principles remain largely consistent.
	- Its power lies in its ability to handle large volumes of data efficiently, perform complex queries, ensure data integrity, and provide a standardized interface for interacting with databases across different platforms and applications.