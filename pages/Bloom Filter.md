tags:: [[Probabilistic Data Structure]]

- # Bloom Filter
	- A Bloom Filter is a probabilistic data structure used for membership testing in a set. It efficiently determines whether an element is present in a set or not, with a possibility of false positives but no false negatives. This means it may incorrectly indicate that an element is in the set, but it will never incorrectly claim that an element is not in the set.
	- ## How a Bloom Filter works
		- **Initialization**
			- Start with an array of bits, initially set to 0, of size `m`.
		- **Hash Functions**
			- Choose `k` different hash functions. These hash functions should be fast and generate uniformly distributed values.
		- **Insertion**
			- To insert an element into the Bloom Filter, hash the element `k` times using the hash functions. Set the bits at the resulting indices to 1.
		- **Membership Testing**
			- To test if an element is in the set, hash the element `k` times using the same hash functions. If all the bits at the resulting indices are 1, the element is considered to be in the set. If any of the bits are 0, the element is definitely not in the set. If all bits are 1, there is a probability of false positive.
		- **False Positive**
			- The probability of a false positive depends on the number of hash functions `k`, the size of the Bloom Filter `m`, and the number of elements in the set `n`. It can be approximated by the formula:
				- $$
				  \left(1 - \left(1 - \frac{1}{m}\right)^{kn}\right)^k
				  $$
					- `m` is the size of the Bloom Filter (number of bits)
					- `k` is the number of hash functions
					- `n` is the number of elements in the set
			- Increasing the size of the Bloom Filter or the number of hash functions reduces the false positive rate but increases memory usage and computational cost.
		- **Applications**
			- Spell checkers
				- To quickly check if a word is misspelled.
			- Web caching
				- To check if a web page is already cached.
			- Network routers
				- To quickly check if a URL is malicious.
		- **Trade-offs**
			- False positives
				- The Bloom Filter can return false positives but never false negatives.
			- Memory usage
				- The Bloom Filter uses a fixed amount of memory, which depends on the desired false positive rate and the number of elements.
			- Deletion
				- It's not possible to delete an element from a Bloom Filter without using additional data structures or resetting the entire Bloom Filter.
	- Overall, Bloom Filters are useful for scenarios where memory efficiency is important, and a small probability of false positives is acceptable.