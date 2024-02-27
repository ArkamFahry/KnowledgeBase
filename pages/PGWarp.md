tags:: [[PostgreSQL]], [[CDC]], [[NATS]]

- # PGWarp
	- A custom implementation of [[CDC]] which subscribes to the [[PostgreSQL WAL]] and pushes these changes into [[NATS]] building a real-time reactive event pipeline for [[PostgreSQL]].