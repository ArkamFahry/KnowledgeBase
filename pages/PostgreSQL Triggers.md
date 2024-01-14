tags:: [[PostgreSQL]]

- # PostgreSQL Triggers
	- PostgreSQL, a trigger is a set of instructions that are automatically executed or fired in response to specific events on a particular table or view. Triggers are used to enforce constraints, implement business rules, and perform actions such as logging changes, updating other tables, or validating data before it is inserted, updated, or deleted.
	- ## Key concepts related to PostgreSQL triggers
		- **Event**
			- Triggers are associated with specific events, such as `INSERT`, `UPDATE`, `DELETE`, or `TRUNCATE` operations on a table. A trigger is executed automatically when the specified event occurs.
		- **Timing**
			- Triggers can be classified based on the timing of their execution:
			- **BEFORE Triggers**
				- These triggers are executed before the actual operation (e.g., before an `INSERT`, `UPDATE`, or `DELETE` statement). They are commonly used to modify the data before it is written to the table.
			- **AFTER Triggers**
				- These triggers are executed after the completion of the operation. They are often used for actions that need to occur after the data has been modified.
		- **Row-level and Statement-level Triggers**
			- **Row-level Triggers**
				- These triggers are executed once for each row affected by the triggering event. They can access the values of the row being modified.
			- **Statement-level Triggers**
				- These triggers are executed once for each triggering event, regardless of the number of rows affected. They cannot access the values of the individual rows.
		- **Trigger Functions**
			- Triggers are associated with trigger functions, which are user-defined functions written in a procedural language such as PL/pgSQL or PL/Tcl. These functions contain the logic that is executed when the trigger is fired.
		- **Trigger Conditions**
			- Triggers can have optional conditions specified using a `WHEN` clause. The trigger function is only executed if the condition evaluates to true. This allows for more fine-grained control over when a trigger should be activated.
	- ## Basic example of a trigger in [[PostgreSQL]]
		- ```sql
		  CREATE OR REPLACE FUNCTION before_insert_trigger()
		  RETURNS TRIGGER AS $$
		  BEGIN
		  -- Your logic here
		  NEW.column_name := 'modified value';
		  RETURN NEW;
		  END;
		  $$ LANGUAGE plpgsql;
		  
		  CREATE TRIGGER example_trigger
		  BEFORE INSERT ON your_table
		  FOR EACH ROW
		  EXECUTE FUNCTION before_insert_trigger();
		  ```
			- In this example, the trigger function `before_insert_trigger` is executed before each `INSERT` operation on `your_table`. It modifies the value of a column before the actual insertion.
	- Triggers provide a powerful mechanism to enforce business rules, maintain data integrity, and automate tasks within a PostgreSQL database. However, it's important to use them judiciously, as improper use can lead to complex and hard-to-maintain database systems.