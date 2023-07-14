- # Genetic Algorithms (GAs): Search based algorithms based on the concepts of natural selection and genetics
	- A genetic algorithm is a search-based [[Heuristic]] algorithm based on [Charles Darwin - Wikipedia](https://en.wikipedia.org/wiki/Charles_Darwin) theory of natural evolution ([Darwinism - Wikipedia](https://en.wikipedia.org/wiki/Darwinism)).
	- The algorithm reflects the process of natural selection where the fittest individuals are selected for reproduction in order to produce offspring of the next generation.
	- ## The Process of Natural Selection
		- The process of natural selection starts with the selection of the fittest individuals from a population. They produce offspring which inherit the characteristics of the parents and will be added to the next generation. If parents have better fitness, their offspring will be better than parents and have a better chance of surviving. This process keeps on iterating and in the end, a generation with the fittest individuals will be found.
		- This notion can be applied to a search problem. The consideration of a set of solutions for a problem and select the set of best ones out of them.
		- ### Five phases of consideration
			- Initial population
			- Fitness function
			- Selection
			- Crossover
			- Mutation
	- ## The Basic idea of a Genetic Algorithm
		- It all starts with a population of randomly generated solutions, called chromosomes. Each chromosome represents a possible solution to the problem. The GA then iteratively applies three main operators to the population.
			- Selection
				- The fittest chromosomes are selected to be parents for the next generation.
			- Crossover
				- The parents' chromosomes are combined to create new chromosomes.
			- Mutation
				- Random changes are introduced to the chromosomes.
		- The process will be repeated until the GA converges on a solution that is good enough, or until a maximum number of iterations is reached.
		- GAs are a powerful tool for solving problems that are difficult to solve using traditional methods.
	- ## The Main Steps of a Genetic Algorithm
		- Some of the main steps of a genetic algorithm
			- Initialize a population of chromosomes.
			  logseq.order-list-type:: number
			- Evaluate the fitness of each chromosome.
			  logseq.order-list-type:: number
			- Select the fittest chromosomes to be parents.
			  logseq.order-list-type:: number
			- Perform crossover on the parents to create new chromosomes.
			  logseq.order-list-type:: number
			- Mutate some of the new chromosomes.
			  logseq.order-list-type:: number
			- Evaluate the fitness of the new chromosomes.
			  logseq.order-list-type:: number
			- Repeat steps 3-6 until the stopping criteria are met.
			  logseq.order-list-type:: number
		- The stopping criteria can be something like a maximum number of generations, a maximum time limit, or a certain fitness threshold.
	- ## Genetic Algorithm Use cases
		- Optimization problems
		- Search problems
		- Machine learning problems
		- Engineering problems
		- Financial problems
	- ## Genetic Algorithm caveats
		- GAs can be computationally expensive, and they may not always converge on the optimal solution.
	- ## Genetic Algorithm Resources
		- [Genetic algorithm - Wikipedia](https://en.wikipedia.org/wiki/Genetic_algorithm)
		- [Genetic Algorithms - Introduction](https://www.tutorialspoint.com/genetic_algorithms/genetic_algorithms_introduction.htm)
		- [Genetic Algorithms - GeeksforGeeks](https://www.geeksforgeeks.org/genetic-algorithms/)