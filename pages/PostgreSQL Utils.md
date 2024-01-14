tags:: [[PostgreSQL]], [[PostgreSQL Functions]]

- ## PostgreSQL Utils
	- ```sql
	  CREATE SCHEMA util;
	  ```
	- ```sql
	  CREATE OR REPLACE FUNCTION util.text_non_empty_trimmed_text(val TEXT) RETURNS BOOLEAN AS
	  $$
	  BEGIN
	      RETURN TRIM(val) <> '';
	  END;
	  $$ LANGUAGE plpgsql;
	  ```
	- ```sql
	  CREATE OR REPLACE FUNCTION util.text_null_or_non_empty_trimmed_text(val TEXT) RETURNS BOOLEAN AS
	  $$
	  BEGIN
	      RETURN val IS NOT NULL AND TRIM(val) <> '';
	  END;
	  $$ LANGUAGE plpgsql;
	  ```
	- ```sql
	  CREATE OR REPLACE FUNCTION util.array_contains_non_empty_trimmed_text(val TEXT[]) RETURNS BOOLEAN AS
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
	- ```sql
	  CREATE OR REPLACE FUNCTION util.array_null_or_contains_empty_trimmed_text(val TEXT[]) RETURNS BOOLEAN AS
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
	- ```sql
	  CREATE OR REPLACE FUNCTION util.array_text_values_unique(val TEXT[])
	      RETURNS BOOLEAN AS
	  $$
	  BEGIN
	      RETURN array_length(val, 1) = array_length(array(SELECT DISTINCT unnest(val)), 1);
	  END;
	  $$ LANGUAGE plpgsql;
	  ```
	- ```sql
	  CREATE OR REPLACE FUNCTION util.set_updated_at()
	  RETURNS TRIGGER AS $$
	  BEGIN
	      new.updated_at = now();
	      RETURN new;
	  END;
	  $$ LANGUAGE plpgsql;
	  
	  
	  CREATE TRIGGER trigger_table_updated_at
	  BEFORE UPDATE ON schema.table
	  FOR EACH ROW
	  EXECUTE FUNCTION util.set_updated_at();
	  ```