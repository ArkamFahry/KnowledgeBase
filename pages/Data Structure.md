tags:: [[DSA]]

- # Data Structure
	- Based on the discussion on [[Data Type]] once we have data in variables. We need a way to manipulating that data to solve problems. This is where **Data Structures** come in. **Data Structures** is a particular way of storing and organizing data in a computer so that it can be used efficiently. A data structure is a special format for organizing and storing data. General data structure types include arrays, files, linked
	  lists, stacks, queues, trees, graphs and so on.
	- Depending on the organization of the elements, data structures are classified into two types
		- Linear data structures
			- Elements are accessed in a sequential order but it is not
			  compulsory to store all elements sequentially. Examples: Linked Lists, Stacks and Queues.
		- Non – linear data structures
			- Elements of this data structure are stored/accessed in a non-linear order. Examples: Trees and graphs.
	- ## Abstract Data Types (ADTs)
		- Before defining abstract data types, let us consider the different view of system-defined data types. We all know that, by default, all primitive data types (int, float, etc.) support basic operations such as addition and subtraction. The system provides the implementations for the primitive data types. For user-defined data types we also need to define operations. The implementation for these operations can be done when we want to actually use them. That means, in general, user defined data types are defined along with their operations. To simplify the process of solving problems, we combine the data structures with their operations and we call this Abstract Data Types (ADTs). An ADT consists of two parts
			- Declaration of data
			- Declaration of operations
		- Commonly used ADTs include: Linked Lists, Stacks, Queues, Priority Queues, Binary Trees, Dictionaries, Disjoint Sets (Union and Find), Hash Tables, Graphs, and many others. For example, stack uses LIFO (Last-In-First-Out) mechanism while storing the data in data structures. The last element inserted into the stack is the first element that gets deleted. Common operations of it are: creating the stack, pushing an element onto the stack, popping an element from stack, finding the current top of the stack, finding number of elements in the stack, etc.
		- While defining the ADTs do not worry about the implementation details. They come into the picture only when we want to use them. Different kinds of ADTs are suited to different kinds of applications, and some are highly specialized to specific tasks. By the end of this book, we will go through many of them and you will be in a position to relate the data structures to the kind of problems they solve.