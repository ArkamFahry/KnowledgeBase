tags:: [[Rust]]

- # Noria: data-flow for high-performance web applications
	- Noria is a new streaming data-flow system designed to act as a fast storage backend for read-heavy web applications based on [Jon Gjengset's Phd Thesis](https://jon.thesquareplanet.com/papers/phd-thesis.pdf), as well as [this paper](https://jon.tsp.io/papers/osdi18-noria.pdf) from [OSDI'18](https://www.usenix.org/conference/osdi18/presentation/gjengset). It acts like a database, but precomputes and caches relational query results so that reads are blazingly fast. Noria automatically keeps cached results up-to-date as the underlying data, stored in persistent *base tables*, change. Noria uses partially-stateful data-flow to reduce memory overhead, and supports dynamic, runtime data-flow and query change.
	- ## Noria Resources
		- [GitHub - mit-pdos/noria: Fast web applications through dynamic, partially-stateful dataflow](https://github.com/mit-pdos/noria)
		- [Noria: dynamic, partially-stateful data-flow for high-performance web applications | USENIX](https://www.usenix.org/conference/osdi18/presentation/gjengset)