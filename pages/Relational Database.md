tags:: [[Database]]

- # Relational Database
	- A relational database is a type of database that stores and organizes data in tables with rows and columns, forming relationships between them. These databases follow the relational model, which was introduced by Edgar F. Codd ([Edgar F. Codd - Wikipedia](https://en.wikipedia.org/wiki/Edgar_F._Codd)) in the 1970s.
	- ## Key components and concepts of a relational database:
		- **Tables**
			- Data is organized into tables, where each table consists of rows (also known as records or tuples) and columns (also known as fields or attributes). Each row represents a single instance of the entity that the table tracks, and each column represents a specific attribute or property of that entity.
		- **Keys**
			- Keys are used to uniquely identify rows within a table. The primary key is a column or set of columns that uniquely identifies each row in a table. Foreign keys establish relationships between tables by referencing the primary key of another table.
		- **Relationships**
			- Relationships are established between tables using keys. Common types of relationships include one-to-one, one-to-many, and many-to-many. These relationships help maintain data integrity and consistency within the database.
		- **Normalization**
			- It's a process to organize the data efficiently by reducing redundancy and dependency. This process involves breaking down large tables into smaller ones and linking them through relationships.
		- **SQL (Structured Query Language)**
			- [[SQL]] is the standard language used to interact with relational databases. It allows users to perform various operations such as querying data, inserting, updating, and deleting records, creating and modifying tables, and defining relationships.
	- Relational databases are widely used due to their flexibility, ease of use, and ability to handle complex queries efficiently. They're used in various applications ranging from small-scale databases to large enterprise systems. Examples of relational database systems include [[MySQL]], [[PostgreSQL]], and [[SQLite]].