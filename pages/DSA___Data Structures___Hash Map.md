# Hash Map
	- A hash map is a data structure used for storing key-value pairs. It's designed to provide rapid insertion, deletion, and lookup of values based on a unique key. The core idea behind a hash map is the use of a technique called hashing, where keys are converted into unique addresses, allowing for quick retrieval of the associated values.
	- ## Breakdown of how a hash map works
		- **Hashing Function**
			- When you add a key-value pair to a hash map, a hashing function is applied to the key. This function generates a unique numerical value, called a hash code or hash value. Ideally, each key generates a unique hash code.
		- **Indexing**
			- The hash code is used to determine the index or storage location within the underlying array or structure of the hash map. This index is where the associated value will be stored.
		- **Storage**
			- The key-value pairs are stored in this structure based on their hashed index. If multiple keys hash to the same index (a collision), most hash maps use additional techniques, like chaining (using linked lists or other structures) or open addressing (finding the next available slot), to manage these collisions.
		- **Retrieval**
			- When you want to retrieve a value associated with a particular key, the hashing function is applied again to the key to find the corresponding index. This allows for rapid lookup of the stored value.
	- Hash maps are commonly used in programming because they offer efficient insertion, deletion, and lookup operations. However, their performance might degrade if there are many collisions, so choosing a good hashing function and handling collisions effectively are important for optimal performance.
	- ## Commonly used hashing methods for hash maps
		- **Division Method**
			- This method involves taking the key, dividing it by the table size, and using the remainder as the hash code. For instance, `hash(key) = key % table_size`. This method is simple but might cause clustering if not implemented properly.
		- **Multiplication Method**
			- It involves multiplying the key by a constant factor, extracting the fractional part, and then multiplying it by the table size. The formula looks like `hash(key) = (a * key) mod 1 * table_size`, where 'a' is a constant between 0 and 1. This method provides better distribution than the division method.
		- **Universal Hashing**
			- It's a family of hash functions that use a randomly chosen hash function from a set of hash functions. This method helps in reducing the chances of collisions significantly.
		- **MurmurHash**
			- MurmurHash is a non-cryptographic hash function that produces a good distribution of hash codes with a low collision rate. It's widely used in hash maps and is known for its speed and effectiveness.
		- **Jenkins Hash Function**
			- This is another non-cryptographic hash function that is simple and fast. It works well for general hash map implementations.
	- ## Hash Map Resources
		- [Hash table - Wikipedia](https://en.wikipedia.org/wiki/Hash_table)