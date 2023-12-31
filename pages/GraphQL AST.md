tags:: [[GraphQL]]

- # GraphQL AST
	- When a [[GraphQL]] server receives a query, it comes in as a single string. This string needs to be broken down into meaningful parts, a process known as tokenization, and then parsed into a format that the machine can understand. This format is called an Abstract Syntax Tree, or AST.
	- The AST is used extensively on the server-side to handle schema definitions and parse the actual GraphQL query. It includes a lot of metadata, such as the location in the source, or identifiers like argument names. The server then traverses the tree, executing each part against the schema.
	- This process of converting raw strings to an AST is the first step of every compiler, from languages like C++ to JavaScript’s VM in Chrome to transpilers like Babel.
	- While this explanation provides a high-level overview, the specifics of how the AST works in GraphQL can get quite complex and involve a deep understanding of compilers and parsing. It’s a fundamental part of how GraphQL processes requests and returns the precise data the client asked for.
	- ## GraphQL AST Resources
		- [How ASTs power the GraphQL schema handling | Contentful](https://www.contentful.com/blog/graphql-abstract-syntax-tree-new-schema/)