tags:: [[PostgreSQL]], [[CDC]], [[NATS]]

- # PGStream
	- A custom implementation of [[CDC]] which subscribes to the [[PostgreSQL WAL]] and pushes these changes into [[NATS]] building a real-time reactive event pipeline for [[PostgreSQL]].
	- ## PGStream Technical Terms
		- Snapshot
			- Snapshot is the process of scanning a full table in [[PostgreSQL]] to get all the data from a table which doesn't exist in the [[PostgreSQL WAL]].
		- Incremental-Snapshot
			- Incremental-Snapshot is the process of scanning a full table in [[PostgreSQL]] block by block without locking the whole table. This is done parallel while reading the [[PostgreSQL WAL]] log.
		- Stream
			- stream is used to describe a stream of event changes from a [[PostgreSQL]] table like `insert`, `update`, `delete`, `truncate`, `snapshot` and `unknown`.
		- Event
			- The message returned for a operation in [[PostgreSQL]] table like `insert`, `update`, `delete`, `truncate`, `snapshot` and `unknown`.
			- Event Format.
				- ```pseudo
				  Event {
				  	id: string -- unique ulid generated for each event
				  	database: string -- database name
				      schema: string -- schema name
				      table: string -- table name
				      operation: string -- operation name in (insert, update, delete, truncate, snapshot, unknown)
				      data: {
				      	before: any -- before data value before the operation if `insert` it will be null
				    		after: any -- after data value after the operation if `delete` it will be null
				      	diff: any -- diff data value is shows the changed value in a `update` operation it will be null if no change
				    	}
				    	timestamp: timestamptz -- timestamp when the event was created this is represented in ISO date time 
				  }
				  ```
		- Subject
			- How a Stream of Database Events are Mapped to a [[NATS Subject]].
			- Subject Format.
				- ```pseudo
				  Subject = database.schema.table.operation
				  ```
	- ## PGStream Requirements
		- Multi-Tenancy. A single instance should be able to interact with multiple [[PostgreSQL]] databases.
		- Watch the [[PostgreSQL WAL]] and publish those [[WAL]] events in to [[NATS]].
		- [[NATS Subject]] mappings for the events would look like `[database].[schema].[table].[operation]`. This can be overridden by custom event mapping or a table could get a totally custom subject name if it's manually defined.
		- Persistent and Ephemeral streams.
			- A stream will default to being persistent but this can be modified per table marking it's  stream as persistent or ephemeral.
			- A persistent stream would be using [[NATS JetStream]] instance.
			- A ephemeral stream would be using [[NATS PubSub]] instance.
		- Snapshots and Incremental-Snapshots.
	- ## PGStream Architecture
		- [[PGStream Architecture]]
	- ## PGStream Resources
		- [GitHub - ArkamFahry/pgstream: A real-time event stream on Postgres powered by CDC and NATS](https://github.com/ArkamFahry/pgstream)