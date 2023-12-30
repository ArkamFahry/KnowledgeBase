tags:: [[DSA]], [[Data Structure]]

- # FIFO Queue (First-In, First-Out Queue)
	- A FIFO queue stands for "First-In, First-Out" queue. It's a [[Data Structure]] in which the first element added to the queue will be the first one to be removed. It operates on the principle that the element that is inserted first will be the one to be taken out first. Think of it like a queue at a ticket counter or a line at a grocery store—the first person to join the line will be the first person to get serviced.
	- In programming, a FIFO queue is often implemented using arrays, linked lists, or other data structures. It supports two main operations:
		- Enqueue
			- This operation adds an element to the end of the queue. It's akin to a person joining the back of the line in a queue.
		- Dequeue
			- This operation removes the element at the front of the queue. It mimics the person at the front of the line getting served and leaving the queue.
	- FIFO queues follow a strict order, ensuring that elements are processed in the same sequence in which they were added. This characteristic makes them suitable for various applications like task scheduling, breadth-first search algorithms, job scheduling, and more.