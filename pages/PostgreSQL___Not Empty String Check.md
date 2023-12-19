# Not Empty String Check
	- It's a pian when debugging if it's `null` or `""` empty string.
	- So this function can preform the check in DB level and not let the insertion of an empty string.
		- ```sql
		  CREATE OR REPLACE FUNCTION not_empty_string(val TEXT) RETURNS BOOLEAN AS $$
		  BEGIN
		      RETURN val <> '';
		  END;
		  $$ LANGUAGE plpgsql;
		  ```
	- Usage Example
		- ```sql
		  CREATE TABLE users (
		      id TEXT PRIMARY KEY CHECK(not_empty_string(id)),
		      name TEXT NOT NULL CHECK(not_empty_string(name)),
		      email TEXT CHECK(not_empty_string(email)),
		      password_hash TEXT CHECK(not_empty_string(password_hash)),
		      phone_number TEXT CHECK(not_empty_string(phone_number))
		  );
		  ```
		- If an insertion is tried with a empty string for example as below
			- ```sql
			  INSERT INTO users (id, name) VALUES ('A1', '');
			  ```
			- Error `new row for relation "users" violates check constraint "users_name_check"` will be thrown and insert will fail.