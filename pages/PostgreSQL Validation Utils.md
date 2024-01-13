tags:: [[PostgreSQL]]

- ## PostgreSQL Validation Utils
	- Non empty trimmed string check
		- ```sql
		  CREATE OR REPLACE FUNCTION util_non_empty_trimmed_string(val TEXT) RETURNS BOOLEAN AS
		  $$
		  BEGIN
		      RETURN TRIM(val) <> '';
		  END;
		  $$ LANGUAGE plpgsql;
		  ```
	- Null or non empty trimmed string check
		- ```sql
		  CREATE OR REPLACE FUNCTION util_null_or_non_empty_trimmed_string(val TEXT) RETURNS BOOLEAN AS
		  $$
		  BEGIN
		      RETURN val IS NOT NULL AND TRIM(val) <> '';
		  END;
		  $$ LANGUAGE plpgsql;
		  ```
	- Array contains empty trimmed string check
		- ```sql
		  CREATE OR REPLACE FUNCTION util_array_contains_empty_trimmed_string(val TEXT[]) RETURNS BOOLEAN AS
		  $$
		  DECLARE
		      i INT;
		  BEGIN
		      FOR i IN ARRAY_LOWER(val, 1) .. COALESCE(ARRAY_UPPER(val, 1), 0) LOOP
		          IF TRIM(val[i]) <> '' THEN
		              RETURN TRUE;
		          END IF;
		      END LOOP;
		  
		      RETURN FALSE;
		  END;
		  $$ LANGUAGE plpgsql;
		  ```
	- Null or array contains empty trimmed string check
		- ```sql
		  CREATE OR REPLACE FUNCTION util_null_or_array_contains_empty_trimmed_string(val TEXT[]) RETURNS BOOLEAN AS
		  $$
		  DECLARE
		      i INT;
		  BEGIN
		      IF val IS NULL THEN
		          RETURN FALSE;
		      END IF;
		  
		      FOR i IN ARRAY_LOWER(val, 1) .. COALESCE(ARRAY_UPPER(val, 1), 0) LOOP
		          IF TRIM(val[i]) <> '' THEN
		              RETURN TRUE;
		          END IF;
		      END LOOP;
		  
		      RETURN FALSE;
		  END;
		  $$ LANGUAGE plpgsql;
		  ```
	- Array contains duplicate value check
		- ```sql
		  CREATE OR REPLACE FUNCTION storage.array_values_are_unique(arr TEXT[])
		      RETURNS BOOLEAN AS
		  $$
		  BEGIN
		      RETURN array_length(arr, 1) = array_length(array(SELECT DISTINCT unnest(arr)), 1);
		  END;
		  $$ LANGUAGE plpgsql;
		  ```