tags:: [[Consensus Algorithms]]

- # Raft
	- [Raft](https://en.wikipedia.org/wiki/Raft_(algorithm)) is a consensus algorithm designed to achieve fault tolerance in distributed systems. It was introduced by Diego Ongaro and John Ousterhout in a 2014 paper titled "[In Search of an Understandable Consensus Algorithm](https://raft.github.io/raft.pdf)" Consensus is a fundamental problem in distributed computing, where a group of nodes must agree on a single value or decision even if some nodes fail or behave incorrectly.
	- Raft is designed to be more understandable than some other consensus algorithms, such as [[Paxos]], and it provides a clear separation between leader election, log replication, and safety properties. The algorithm is divided into three main components:
		- **Leader Election**
			- In Raft, one node serves as the leader, and it is responsible for coordinating the activities of the cluster. The leader is elected through a process in which nodes exchange heartbeat messages, and if a node does not receive a heartbeat from a leader for a certain period (election timeout), it starts a new election.
			- During an election, nodes request votes from other nodes, and a node becomes the leader if it receives votes from a majority of the nodes.
		- **Log Replication**
			- The distributed log is the core of Raft, representing a sequence of commands that need to be executed on each node. The leader receives client requests and appends them to its log. It then replicates the log entries to other nodes.
			- Raft ensures that logs are consistent across nodes through a mechanism called log replication. Nodes replicate log entries from the leader and apply them to their state machines in the same order, guaranteeing consistency.
		- **Safety**
			- Raft ensures safety properties, such as ensuring that once a log entry is committed by a leader, it is guaranteed to be present in the logs of a majority of the nodes. This prevents the system from losing committed data even in the presence of node failures.
	- ## Raft Resources
		- [Raft Consensus Algorithm](https://raft.github.io/)
		- https://raft.github.io/raft.pdf
		- [Raft consensus algorithm website · GitHub](https://github.com/raft)
	- Raft provides a straightforward and understandable approach to distributed consensus, making it easier to reason about and implement. It has been used in various distributed systems to provide fault tolerance and consistency, such as in distributed databases and distributed storage systems.