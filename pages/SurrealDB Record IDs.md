# SurrealDB Record IDs: The Magic behind [[SurrealDB]]
	- ## SurrealDB Record IDs
		- SurrealDB Record IDs are represented as `table:id` making them efficient query directly and these IDs can range from simple to complex. These IDs make it possible to Fetch relations without joins.
		- ### Text Record IDs
			- Without annotation, text record IDs can contain letters, numbers and `_` characters.
				- ```sql
				  CREATE oragnizations:axiomlab SET name = 'AxiomLab';
				  ```
			- Record IDs can contain complex characters, surrounded by the `` character.
				- ```sql
				  CREATE product:`8424486b-85b3-4448-ac8d-5d51083391c7` SET 
				  	created_at = time::now(), 
				      category = packages:axios;
				  ```
			- Alternatively complex characters within record IDs can be surrounded by the `⟨` and `⟩` characters.
				- ```sql
				  CREATE meassages:⟨8424486b-85b3-4448-ac8d-5d51083391c7⟩ SET 
				  	created_at = time::now(), 
				      creator = users:arkam;
				  ```
		- ### Numeric Record IDs
			- If a numeric value is specified without any decimal point suffix and is within the range `-9223372036854775808` to `9223372036854775807` then the value will be parsed, stored, and treated as a 64-bit integer.
				- ```sql
				  CREATE logs:17493 SET 
				  	metadata = {
				      	server_log: 'the server crached and died',
				          error: 'death'
				      }, 
				      created_at = time::now();
				  ```
			- SurrealDB doesn't have in built auto increment IDs because of it's distributed nature.
			  background-color:: yellow
		- ### Object-based Record IDs
			- Complex Record IDs support dynamic expressions, allowing parameters, and function expressions to be used as values within the IDs. This is useful in a timeseries context, or for ensuring locality between specific records in a table.
			- This will represented with `table name:{ the object based ID }`.
				- ```sql
				  // Create a record with a complex ID using an object
				  CREATE oragnizations:{ 
				  	tenant_id: '8424486b-85b3-4448-ac8d-5d51083391c7', 
				      name: 'AxiomLabs' 
				  } SET
				  	description = 'A company which builds cool stuff',
				  	created_at = time::now()
				  ;
				  ```
		- ### Array-based Record IDs
			- Complex Record IDs support dynamic expressions, allowing parameters, and function expressions to be used as values within the IDs. This is useful in a timeseries context, or for ensuring locality between specific records in a table.
				- ```sql
				  // Set a new parameter
				  LET $now = time::now();
				  
				  // Create a record with a complex ID using an array
				  CREATE temperature:['London', $now] SET
				  	location = 'London',
				  	date = $now,
				  	temperature = 23.7
				  ;
				  ```
		- ### Generating Record IDs
			- Record IDs can be generated with a number of built-in ID generation functions. These allow for Record IDs to be generated using cryptographically-secure randomly-generated identifiers (which are suitable for dispersion across a distributed datastore), sequentially incrementing `ULID` Record identifiers, and `UUID` version 7 Record idenfitifiers.
				- ```sql
				  // Generate a random Record ID
				  CREATE temperature:rand() SET 
				  	created_at = time::now(), 
				      name = 'tester1';
				  
				  // Generate a ULID-based Record ID
				  CREATE temperature:ulid() SET 
				  	created_at = time::now(), 
				      name = 'tester2';
				   
				  // Generate a UUIDv7-based Record ID
				  CREATE temperature:uuid() SET 
				  	created_at = time::now(), 
				      name = 'tester3';
				  ```
			- If possible always use `ULID` or `UUIDv7` because they are sortable meaning they are more preferment than  random `UUID`'s when querying the database.