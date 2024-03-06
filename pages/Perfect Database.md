tags:: [[Database]], [[NewSQL]]

- # Perfect Database
	- ## Features of a perfect database
	  id:: 65e48511-2c0f-42e8-8eb3-fc305192f2ee
		- Database should have storage and compute separated.
		- Database should be document based with inter document relationship support meaning the database should be a document relational database.
		- Database should support schema less, partial schemas and full schema support.
		- Database should generate schema on the fly by smartly introspecting and detecting what data is in a table and generates a schema.
		- Database should be reactive meaning any query to the database should be able to turn into a subscription query which returns data in real-time.
		- Database should have a directly usable and reliable [[CDC]] stream.
		- Database should should have reliable event triggers which can be used by applications to listen to database changes.
		- Database should support computed fields.
		- Database should support [[Incremental Materialized View]]'s.
		- Database should be [[ACID]] compliant.
		- Database should support strictly [[Serializable Transaction]] with [[DOCC]] with automatic transaction retries. This means database supports the highest level of consistency with the highest level of concurrency.
		- Database should support full-text search and vector search natively.
		- Database should support for running delayed database mutations and queries.
		- Database should generate fully type safe clients for any language.
		- Database should have native soft deletes and ability to set when to permanent the soft delete.
		- Database should support native versioning of data to track all changes. meaning we can get audit history of every change to the data.
		- Database should support native TTL for data with permanent and soft delete.
		- Database should support native object storage.
		- Database should support native dataflow based caching which are automatically maintained.
		- Database should have data consistency not only on the database level. The data should be consistent up to the application level meaning the database should keep application state consistent with database state at all time.
		- Database support running serverless functions literally in the database right next to the data making the functions fast as possible.
			- Database should use the database guarantees to execute code as workflows.
			- Database functions should have the ability to run functions on database events reacting to database changes.
			- Database functions should have the ability to have auto retries with exponential backoff on functions without extra config.
		- Database should have the Ability to run [[WASM]] modules directly in the database.