- # SQLite Data Types: The weird world of Data Types in SQLite
	- ## Data Types in SQLite
		- Most [[SQL]] database engines have static rigid type system where the data type of a value is determined by its container which means the particular column in which the value is stored while [[SQLite]] type system is flexible.
		- [[SQLite]] uses a more general dynamic type system. In SQLite, the datatype of a value is associated with the value itself, not with its container. The dynamic type system  is backwards compatible with the more common static type systems of other database engines in the sense that SQL statements that work on statically typed databases work the same way in SQLite.
		- However, the dynamic typing in SQLite allows it to do things which are not possible in traditional rigidly typed databases. This could be a double sided blade this gives the ability store dynamic data all the while at the cost of sacrificed safety.
	- ## Storage Classes and Data Types
		- Each value stored in an SQLite database has one of the following storage classes
			- **NULL**
				- The value is a  *NULL* value
			- **INTEGER**
				- The value is a *signed integer*, stored in *0, 1, 2, 3, 4, 6, or 8 bytes* depending on the magnitude of the value.
			- **REAL**
				- The value is a *floating point value*, stored as an *8-byte IEEE floating point number*.
			- **TEXT**
				- The value is a *text string*, stored using the database encoding *(UTF-8, UTF-16BE or UTF-16LE)*.
			- **BLOB**
				- The value is a *blob of data*, *stored exactly as it was input*.
		- A storage class is more general than a datatype. The INTEGER storage class, for example, includes 7 different integer datatypes of different lengths. But as soon as INTEGER values are read off of disk and into memory for processing, they are converted to the most general datatype (8-byte signed integer). So for the most part, *storage class* is indistinguishable from *data type* and the two terms can be used interchangeably.
		- Any column in an SQLite version 3 database, except an INTEGER PRIMARY KEY column, may be used to store a value of any storage class.
		- All values in SQL statements, whether they are literals embedded in SQL statement text or parameters bound to precompiled SQL statements have an implicit storage class. Under circumstances described below, the database engine may convert values between numeric storage classes (INTEGER and REAL) and TEXT during query execution.
	- ## More detailed Data Types
		- ### Boolean Data Type
			- SQLite does not have a separate Boolean storage class. Instead, Boolean values are stored as integers 0 (false) and 1 (true).
			- SQLite recognizes the keywords "TRUE" and "FALSE" but those keywords are really just alternative spellings for the integer literals 1 and 0 respectively.
		- ### Date and Time Data Type
			- SQLite does not have a storage class set aside for storing dates and/or times. Instead, the built-in Date And Time Function of SQLite are capable of storing dates and times as TEXT, REAL, or INTEGER values.
				- **TEXT** as ISO8601 strings ("YYYY-MM-DD HH:MM:SS.SSS").
				- **REAL** as Julian day numbers, the number of days since noon in Greenwich on November 24, 4714 B.C. according to the proleptic Gregorian calendar.
				- **INTEGER** as Unix Time, the number of seconds since 1970-01-01 00:00:00 UTC.
			- Applications can choose to store dates and times in any of these formats and freely convert between formats using the built-in Date And Time Functions.
		- ### Type Affinity
			- SQL database engines that use rigid typing will usually try to automatically convert values to the appropriate datatype. Consider the below
				- ```sql
				  create table t (
				  	a int,
				    	b varchar(10)
				  );
				  
				  insert into t(a, b) values ('123', 456);
				  ```
				- Rigidly-typed database will convert the string '123' into an integer 123 and the integer 456 into a string '456' prior to doing the insert.
			- In order to maximize compatibility between SQLite and other database engines, and so that the example above will work on SQLite as it does on other SQL database engines, SQLite supports the concept of "type affinity" on columns. The type affinity of a column is the recommended type for data stored in that column. The important idea here is that
			  the type is recommended, not required. Any column can still store any type of data. It is just that some columns, given the choice, will prefer to use one storage class over another. The preferred storage class for a column is called its "affinity".
			- Each column in an SQLite 3 database is assigned one of the following type affinities
				- TEXT
					- A column with TEXT affinity is capable of storing data of different types, including NULL, TEXT, or BLOB. However, when numerical data is inserted into a column with TEXT affinity, it is automatically converted into its text form before being stored. This conversion ensures that all data in the column is consistently stored as text, regardless of its original type.
				- NUMERIC
					- A column with NUMERIC affinity can store values from all five storage classes, including NULL, INTEGER, REAL, TEXT, and BLOB. When text data is inserted into a NUMERIC column, SQLite performs conversions based on specific rules
						- If the text is a well-formed integer literal, it is converted to INTEGER if it fits within a 64-bit signed integer. Otherwise, it is converted to REAL.
						- If the text is a well-formed real literal, it is converted to REAL.
						- When converting between TEXT and REAL storage classes, only the first 15 significant decimal digits of the number are preserved.
						- If the text is not a well-formed integer or real literal, it is stored as TEXT.
						- Hexadecimal integer literals are always stored as TEXT for compatibility with older versions of SQLite.
						- If a floating point value can be represented exactly as an integer, it is converted to INTEGER.
						- NULL and BLOB values are not converted.
						- These rules ensure that the data in a NUMERIC column is stored appropriately based on its content and type, maintaining compatibility and consistency within the database.
					- When a string appears to be a floating-point literal with a decimal point and/or exponent notation, but the value can be expressed as an integer, the NUMERIC affinity will convert it into an integer. For example, the string '3.0e+5' will be stored as the integer 300000, not as the floating point value 300000.0. This behavior ensures that numerical values that can be represented as integers are stored as such, even if they are initially provided in a floating-point format.
				- INTEGER
					- A column with INTEGER affinity behaves the same as a column with NUMERIC affinity. The difference between them becomes evident when using a CAST expression.
						- When using the CAST expression, "CAST(4.0 AS INT)" will return the integer value 4, while "CAST(4.0 AS NUMERIC)" will preserve the value as a floating-point 4.0. This means that INTEGER affinity treats values as integers, while NUMERIC affinity allows for both integer and floating-point representations. However, in terms of storing and manipulating data within the column, INTEGER and NUMERIC affinities behave identically.
				- REAL
					- A column with REAL affinity behaves similarly to a column with NUMERIC affinity, with one key difference. REAL affinity forces integer values to be represented as floating point numbers.
						- As an internal optimization, small floating point values without fractional components are stored as integers on disk when the column has REAL affinity. This optimization reduces the storage space required. When reading the value from the database, it is automatically converted back into a floating point representation.
						- This optimization is transparent at the SQL level, meaning it cannot be observed or controlled directly through SQL statements. It can only be detected by examining the raw binary data of the database file.
				- BLOB
					- A column with BLOB affinity does not favor any specific storage class over another. It does not attempt to coerce or convert data from one storage class to another. This means that data inserted into a column with BLOB affinity will be stored as-is, without any modification or conversion. The BLOB affinity simply treats the data as binary large objects, allowing for flexibility in storing various types of binary data.
			- #### Determination Of Column Affinity
				- When defining a table not as STRIC, the affinity of a column is determined by the declared type of the column, following the following rules in a specific order:
					- If the declared type contains the string "INT", the column is assigned INTEGER affinity.
					  logseq.order-list-type:: number
					- If the declared type contains any of the strings "CHAR", "CLOB", or "TEXT" (including VARCHAR), the column is assigned TEXT affinity.
					  logseq.order-list-type:: number
					- If the declared type contains the string "BLOB" or if no type is specified, the column is assigned BLOB affinity.
					  logseq.order-list-type:: number
					- If the declared type contains any of the strings "REAL", "FLOA", or "DOUB", the column is assigned REAL affinity.
					  logseq.order-list-type:: number
					- If none of the above rules match, the affinity is assigned NUMERIC.
					  logseq.order-list-type:: number
				- It is important to note that the order of the rules is significant. If a declared type matches multiple rules, the first applicable rule takes precedence. For example, if the declared type is "CHARINT," it matches both rules 1 and 2, but the first rule (integer affinity) takes precedence, resulting in the column being assigned INTEGER affinity.
				- Affinity Name Examples
					- The following table shows how many common datatype names from more traditional SQL implementations are converted into affinities by the five rules of the previous section. This table shows only a small subset of the datatype names that SQLite will accept
						- |Type names from The CREATE TABLE statement or CAST expression|Resulting affinity|Rule used to determine affinity|
						  |--|--|--|
						  |INT, INTEGER, TINYINT, SMALLINT, MEDIUMINT, BIGINT, UNSIGNED BIG INT, INT2, INT8|INTEGER|1|
						  |CHARACTER(20), VARCHAR(255), VARYING CHARACTER(255), NCHAR(55), NATIVE CHARACTER(70), NVARCHAR(100), TEXT, CLOB|TEXT|2|
						  |BLOB, no datatype specified|BLOB|3|
						  |REAL, DOUBLE, DOUBLE PRECISION, FLOAT|REAL|4|
						  |NUMERIC, DECIMAL(10,5), BOOLEAN, DATE, DATETIME|NUMERIC|5|
						- Note that a declared type of "FLOATING POINT" would give INTEGER affinity, not REAL affinity, due to the "INT" at the end of "POINT". And the declared type of "STRING" has an affinity of NUMERIC, not TEXT.