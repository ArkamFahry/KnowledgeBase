tags:: [[PostgreSQL]], [[Incremental Materialized View]]

- # PostgreSQL pg_ivm
	- ## What is pg_ivm
		- pg_ivm is a PostgreSQL extension that provides a mechanism for efficiently maintaining materialized views. Materialized views are pre-computed results of queries stored as database tables, offering faster query performance by bypassing the need to re-run the original query on the underlying base tables. However, keeping materialized views synchronized with base tables after modifications can be a challenge.
	- ## How pg_ivm Works
		- pg_ivm employs Incremental View Maintenance (IVM), a technique that updates materialized views only with the incremental changes (inserts, updates, deletes) in the base tables, rather than recomputing the entire view from scratch. This significantly improves performance, especially when dealing with frequently updated base tables or large views.
	- ## Key Concepts
		- **Incrementally Maintainable Materialized View (IMMV)**
			- A materialized view created using pg_ivm to enable incremental updates.
		- **Immediate Maintenance**
			- The approach used by pg_ivm, where the view is updated within the same transaction that modifies the base table. This ensures the view reflects the latest changes as soon as possible.
	- ## Creating IMMVs with pg_ivm
		- pg_ivm provides the `create_immv` function to create IMMVs. It takes two arguments:
			- **IMMV name**
				- The name you assign to the materialized view.
		- **View definition query**
			- The SQL query that defines the view's logic.
		- **Example**
			- ```
			  SELECT create_immv('my_immv', 'SELECT * FROM my_table');
			  ```
				- This creates an IMMV named `my_immv` based on the query `SELECT * FROM my_table`.
	- ## Benefits of pg_ivm
		- **Improved Performance**
			- Updates are faster as only incremental changes are applied.
		- **Reduced Load on Base Tables**
			- Less frequent full recomputations minimize the impact on base tables.
		- **Data Consistency**
			- Ensures materialized views always reflect the latest data.
	- ## PostgreSQL Incremental View Maintenance Resources
		- [GitHub - sraoss/pg_ivm: IVM (Incremental View Maintenance) implementation as a PostgreSQL extension](https://github.com/sraoss/pg_ivm)