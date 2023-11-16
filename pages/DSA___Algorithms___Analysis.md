# Algorithm analysis
	- the process of determining how processing time increases as the size of the problem (input size) increases. Input size is the number of elements in the input, and depending on the problem type, the input may be of different types. The following are the common types of inputs.
		- Size of an array
		- Polynomial degree
		- Number of elements in a matrix
		- Number of bits in the binary representation of the input
		- Vertices and edges in a graph
	- ## Rate of growth
		- The rate at which the running time increases as a function of input is called rate of growth.
		- assume that you go to a shop to buy a PC and a PS5. If your friend sees you there and asks what you are buying, then in general you say buying a PC. This is because the cost of the PC is high compared to the cost of the PS5 (approximating the cost of the PS5 to the cost of the PC)
			- $$
			  Total\_Cost = cost\_of\_PC + cost\_of\_PS5
			  \\
			  Total\_Cost = cost\_of\_PC(approximation)
			  $$
		- For the above-mentioned example, we can represent the cost of the PC and the cost of the PS5 in terms of function, and for a given function ignore the low order terms that are relatively insignificant (for large value of input size, $$n$$). As an example, in the case below, $$n^4$$, $$2n^2$$, $$100n$$ and $$500$$ are the individual costs of some function and approximate to $$n^4$$ since $$n^4$$ is the highest rate of growth.
			- $$n^4 + 2n^2 + 100n + 500 = n^4$$
		- ### Commonly Used Rates of Growth