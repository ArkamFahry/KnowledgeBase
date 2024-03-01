tags:: [[PostgreSQL]], [[PostgreSQL Logical Replication]]

- # PostgreSQL Replication Slot
	- A PostgreSQL Replication Slot is a persistent configuration object that represents a point in the [[WAL]] (Write-Ahead Logging) stream. It's used in logical replication to keep track of the point up to which a replica has consumed changes, ensuring that the changes are retained in the WAL until all replicas have processed them.
	- ## How PostgreSQL Replication Slot works
		- **Creation**
			- When you create a logical replication subscription on a replica, PostgreSQL automatically creates a replication slot associated with that subscription on the primary server.
		- **Retention**
			- The replication slot retains [[WAL]] records on the primary server, even after they have been consumed by all replicas, until the slot is explicitly dropped or becomes inactive due to inactivity_timeout.
		- **Preventing Data Loss**
			- Replication slots help prevent data loss by ensuring that the primary server retains enough [[WAL]] data to allow a replica to catch up even if it goes offline for a period of time.
		- **Monitoring**
			- You can monitor the status of replication slots using PostgreSQL's system views, such as pg_replication_slots. This allows you to see which slots are active, how much WAL data they've retained, and whether they're preventing the removal of older WAL segments.
		- **Limitations**
			- Replication slots consume disk space on the primary server, so it's important to monitor them and drop slots that are no longer needed to avoid running out of disk space. Additionally, if a replication slot is not consumed by any replica for a certain period of time (controlled by the inactivity_timeout setting), it will be automatically removed.
	- Overall, replication slots are a critical component of the [[PostgreSQL Logical Replication]] mechanism, ensuring that changes made on the primary server are reliably replicated to all replicas, even in the presence of network issues or replica downtime.