tags:: [[CRDT]]

- # [[CRDT]] Data Type
	- Counter CRDT
		- Increment-Only Counter
			- This CRDT type only allows incrementing the counter. It ensures that each replica can independently increment its counter, and all replicas eventually converge to the same value, regardless of the order of increments.
	- Set CRDT
		- Two-Phase Set (2P-Set)
			- Consists of an "add set" and a "remove set." Elements can be added to the set, and once removed, they cannot be added again. It ensures that the union of add sets across replicas converges to the same state, handling additions and removals without conflicts.
		- Observed-Remove Set (OR-Set)
			- Allows elements to be added and removed with unique identifiers. This enables safe removal of elements by marking them with unique identifiers, preventing re-addition of removed elements while allowing concurrent additions.
	- Map CRDT
		- Map-based CRDT
			- Provides a way to represent key-value pairs while ensuring conflict-free updates. Operations like adding, removing, or updating key-value pairs can be performed concurrently across replicas without conflicts.
	- Sequence CRDT
		- List CRDT
			- Represents an ordered list where elements can be concurrently added or removed at different positions in the list. Each operation is designed to be commutative, ensuring eventual convergence to the same list across replicas.
	- Register CRDT
		- Last-Writer-Wins Register (LWW-Register)
			- A register that stores a value with a timestamp or version. In case of concurrent updates, the value with the latest timestamp or version is considered the valid value.
	- G-Counter and PN-Counter
		- G-Counter (Grow-Only Counter)
			- Similar to a counter CRDT but allows incrementing and merging of counts across replicas.
		- PN-Counter (Positive-Negative Counter)
			- Extends the G-Counter to allow both increments and decrements while maintaining the ability to merge counts across replicas.