- # PlanetScale Operating Without Foreign Keys
  title:: PlanetScale/Operating Without Foreign Keys
	- ## Why No Foreign Key Support
		- There are two major technical reasons
			- The way `FOREIGN KEY` constraints are implemented in MySQL (or, rather, in the InnoDB storage engine) interferes with Online DDL operations. Learn more in [this Vitess blog post](https://vitess.io/blog/2021-06-15-online-ddl-why-no-fk/).
			- Limited to single MySQL server scope, `FOREIGN KEY` constraints are impossible to maintain once your data grows and is split over multiple database servers. This typically happens when you introduce functional partitioning/sharding and/or horizontal sharding.
		- The advantages of Online DDL such as branching, developer-owned schema
		  changes and deployments, non-blocking schema changes, etc., and the advantages of sharding
		  as means of unlimited scaling, outweigh the `FOREIGN KEY` constraints benefits. In other words, if someone is ready to enforce referential integrity at the application level instead of at the database level, which will open the door to all of those benefits.
		- > No foreign keys doesn't mean demoralizing data or doing some weird data access pattern. The thinking pattern will still be relational but without `FOREIGN KEY` constraints described in the table.
	- ## How Foreign Keys work in MySQL
		- Consider the following `parent` and `child` table relationship
			- ```sql
			  CREATE TABLE parent (
			  	id INT NOT NULL,
			  	PRIMARY KEY (id)
			  );
			  
			  CREATE TABLE child (
			  	id INT NOT NULL,
			  	parent_id INT,
			  	PRIMARY KEY (id),
			    	KEY parent_id_idx (parent_id),
			  	CONSTRAINT `fk_child_parent` FOREIGN KEY (parent_id) REFERENCES parent(id) ON
			  );
			  ```
			- With the `FOREIGN KEY` constraint available  row deletion `ON DELETE` and for row update `ON UPDATE` operations will be available. `ON DELETE` is the commonly used operation and it support three types of functions `ON DELETE CASCADE`, `ON DELETE SET NULL`, `ON DELETE NO ACTION` below these action are described in detail.
				- `ON DELETE CASCADE`
					- In this case if  the deletion of  parent table row happens any referencing rows in child tables are subsequently deleted within the same transaction.
					- This operation run recursively for all of a parent's children, as well as for their children should they also employ `ON DELETE CASCADE`.
					- This is a risky operation.
						- There can be a lot of resource usage if there is lot of cascades. Lets get a scenario, intention is to `DELETE` a single row but this ends up deleting hundreds, thousands or millions of rows in multiple tables. What seemed like a simple transaction now turns into a massive operation, that involves excessive locking,
						  increased MVCC overhead, impact on replication lag, explosions, and more unpleasant things.
						- The biggest risk is potential unexpected loss of data. Whether an
						  unsuspecting developer simply assumes a 
						  ```sql 
						  DELETE FROM parent WHERE id = 3;
						  ```
						  This will at most delete one row, down to surprising behavior such as in REPLACE INTO queries, which actually run
						  an implicit DELETE, leading to mass destruction of data.
					- The use of `ON DELETE CASCADE` is controversial. So use it with caution.
				- `ON DELETE SET NULL`
					- This will set the referencing columns in the children tables to NULL if the parent row is deleted. It effectively orphans the children rows. This is just like not having Foreign keys constraints at all.
					- One advantage is that it's easy to identify the orphan rows those, and only those rows, will have NULL for parent-referencing columns.
					- Like `ON DELETE CASCADE`, a single row deletion on the parent may lead to multiple rows updated on child tables. This again may cause large transactions, excessive locking, explosions, and replication lag.
				- `ON DELETE NO ACTION`
					- The most important feature of foreign keys, a `DELETE` on a parent would fail if a child rows exist. This means to delete a row from the parent there must first be a deletion of all referencing children rows. If the children rows have grandchildren rows they also have to be deleted, so on and so forth.
					- This lack of action type forces the application to have stronger ownership of its data. An app written to work with `ON DELETE NO ACTION` will organically evolve knowing which tables reference
					  which other tables, and will have established DELETE/UPDATE flows that iterate through tables in the correct order to satisfy referential integrity.
	- ## How to Operate Without Foreign Keys
		- The above database schema minus the `CONSTRAINT` clause.
			- ```sql
			  CREATE TABLE parent (
			  	id INT NOT NULL,
			  	PRIMARY KEY (id)
			  );
			  
			  CREATE TABLE child (
			  	id INT NOT NULL,
			  	parent_id INT,
			  	PRIMARY KEY (id),
			    	KEY parent_id_idx (parent_id)
			  );
			  ```
		- Consider application behavior as `ON DELETE NO ACTION` as the scenario.
			- We give the application the know how of the table's dependencies, handles iteration order for `DELETE`/`UPDATE`. It does everything right.
			- At this point if  we take away the `CONSTRAINT`. The app remains unchanged. It already runs the proper actions in the proper order. The application operation that ends up running the 
			  ```sql
			  DELETE FROM parent WHERE id = 3;
			  ```
			  succeeds the application operations that DELETE the child table(s).
			- Likewise, an app that grows with a constraint-less schema organically learns to handle `DELETE` and `UPDATE` scenarios. It is in fact given some extra freedom because the order of operations is not enforced. This is an advantage because the app is not forced to `DELETE` thousands of dependent rows for each parent row deletion at that same transaction. The app may well postpone deletion as we discuss shortly
			- Referential integrity is but one of many logical data integrity constraints. It just happens to be one that databases can enforce. Any sizeable application will maintain the integrity of its data with rules the database is unaware of.
		- ### Clean the orphaned rows
			- Consider an `ON DELETE SET NULL` constraint. What happens to the child rows that were set to NULL? Typically, there is little or no damage in keeping them around. A query can, for example, 
			  ```sql
			  SELECT rows WHERE parent_id IS NOT NULL;
			  ```
			   Better yet, child rows are often JOINed with their respective parent rows. Any query running such a JOIN will return empty since the parent row does not exist.
			- Eventually there will be a pile up of these orphaned rows.
				- Without `FOREIGN KEY` constraints, the situation is very much the same, It is possible to `DELETE` a parent row without deleting its dependent children rows. A child row `JOIN`ed with a respective (deleted) parent row comes out empty. There is no `IS NOT NULL` to help you, but identifying those rows is still trivial. Similarly, there is little or no damage in keeping those rows around for a while.
				- We will want to reclaim that space.
					- A common practice, where appropriate, is to `DELETE` rows on a parent table, or perhaps also on a subset of children, but leave some other tables for offline batch processing. At some convenient time, such as low traffic hours, the app or some batch job will purge orphaned rows. Consider this.
					  ```sql
					  DELETE FROM child LEFT JOIN parent 
					  	ON (child.parent_id = parent.id) 
					  WHERE parent.id IS NULL;
					  ```
					- A single `DELETE` would likely be a massive operation, which is to be avoided. A good practice is to break the statement into multiple small-scope statements. For example limit the deletes to be 100 at a time.
					  ```sql
					  DELETE FROM child LEFT JOIN parent 
					  	ON (child.parent_id = parent.id) 
					  WHERE parent.id IS NULL LIMIT 100;
					  ```