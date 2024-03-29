tags:: [[Probabilistic Data Structure]]

- # Cuckoo Filter
	- Cuckoo Filter is a probabilistic data structure that provides a space-efficient solution for set membership queries with a trade-off of a low false positive rate. It is based on the cuckoo hashing technique and is designed to be more memory-efficient than [[Bloom filter]]s while maintaining similar performance characteristics.
	- ## How Cuckoo Filter works
		- **Initialization**
			- Start with an array of buckets, each containing a small number of slots (typically 2 to 4). Each slot can hold an item or be empty. Also, choose a fingerprint size (usually a few bits) to store a hash of the item.
		- **Insertion**
			- To insert an item, compute its fingerprint using a hash function.
			- Try to insert the item into the bucket corresponding to the hash of the item's fingerprint. If there is an empty slot, insert the item and return success.
			- If the bucket is full, select a random item from the bucket, replace it with the new item, and insert the displaced item into its alternative bucket (computed using a different hash function). Repeat this process recursively until an empty slot is found or a maximum number of displacements is reached.
		- **Lookup**
			- To check if an item is in the filter, compute its fingerprint.
			- Check both possible buckets for the fingerprint. If any bucket contains the fingerprint, return true. Otherwise, return false.
		- **Deletion**
			- Cuckoo Filters do not support deletion of individual items. However, they can support deletion by using a separate data structure to keep track of deleted items.
		- **False Positive Rate**
			- The false positive rate of a Cuckoo Filter depends on the number of buckets, the number of slots per bucket, and the fingerprint size.
			- With suitable parameters, Cuckoo Filters can achieve false positive rates comparable to Bloom filters but with less memory overhead.
		- **Applications**
			- Cuckoo Filters are suitable for applications where memory efficiency is important, such as network routers, distributed systems, and databases.
	- In summary, Cuckoo Filter is a space-efficient probabilistic data structure that provides fast set membership queries with a low false positive rate. It improves upon the [[Bloom Filter]] by using cuckoo hashing and bucket-based storage, making it suitable for applications requiring high memory efficiency.