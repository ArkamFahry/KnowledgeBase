- # How to structure a Go project
	- The structure your Go applications should follow is a somewhat contentious subject. Some people are adamant that everyone should follow the well known [golang-standards/project-layout](https://github.com/golang-standards/project-layout) structure for absolutely every project.
	- With the introduction of [[Go/Modules]] as the standard going forward for handling dependencies, this structure starts to present challenges. Going with the traditional structure, you will find that some folders within your structure will not have access to folders such as `internal` or `pkg` and you will have to implement somewhat hacky solutions in order for these to work as-is.
	- ## Small Project: Flat File Structure
		- A project could start small and grow gradually in this case a flat file structure is preferable in the start.
			- ```
			  app/
			  	main.go
			      main_test.go
			      util.go
			      util_test.go
			      ...
			  ```
			- Starting with a flat folder structure in these situations like the one outlined above is highly preferable. Keeping the structure of your project simple, to begin with. This unlocks the ability to deliver the highest value features to your intended audience as quickly as possible, without the cognitive overhead of a complex structure.
		- ### Benefits
			- Ideal for
				- Microservices
					- tiny applications deployed in a distributed fashion that are built to do one thing, and one thing only.
				- Small Tools and libraries
					- Command line tools or small libraries that focus on doing a handful of tasks really well.
		- ### Examples
			- [GitHub - tidwall/gjson: Get JSON values quickly - JSON parser for Go](https://github.com/tidwall/gjson)
			- [GitHub - go-yaml/yaml: YAML support for the Go language.](https://github.com/go-yaml/yaml)
	- ## Medium/Large Sized Applications: Modularization Structure
		- The project grows to modularize the functionality of the project.
			- ```
			  project_name/
			  	apis/
			      	routes.go
			          routes_test.go
			  	cmd/
			      	main.go
			          main_test.go
			  	util/
			      	utils.go
			          utils_test.go
			      storage/
			      	db.go
			          db_test.go
			    	routes/
			      	user.go
			          user_test.go
			          admin.go
			          admin_test.go
			      public/
			      	models/
			          	user.go
			              admin.go
			              roles.go
			              articles.go
			  	iternals/
			      	hasher.go
			  ```
			- This can potentially centralise any core logic shared across these components into a shared package within the project.
		- ### Examples
			- [GitHub - google/go-cloud: The Go Cloud Development Kit (Go CDK): A library and tools for open cloud development in Go.](https://github.com/google/go-cloud)
			- [GitHub - hashicorp/consul: Consul is a distributed, highly available, and data center aware solution to connect and configure applications across dynamic, distributed infrastructure.](https://github.com/hashicorp/consul)
			- [GitHub - ipfs/kubo: An IPFS implementation in Go](https://github.com/ipfs/go-ipfs)
			- [GitHub - gohugoio/hugo: The world’s fastest framework for building websites.](https://github.com/gohugoio/hugo)