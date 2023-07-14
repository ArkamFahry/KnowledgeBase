- # Go Modules: A module is a collection of Go packages
  title:: Go/Modules
	- ## Go Modules
		- Go modules are a way to manage and organize the external packages or modules that your [[Go]] programs depend on. They help you keep track of which versions of packages that are being used. They simplify the process of managing dependencies, ensuring that your program can be built and run consistently across different environments.
	- ## Go Module Timeline
		- Go module's preliminary support was introduced in Go versions 1.11 and 1.12 as the new [new dependency management system](https://blog.golang.org/versioning-proposal) for Go to simplify dependency management in Go projects. They provide a way to define, version, and manage external packages or modules used in Go programs.
		- Before Go modules, dependencies were managed using the `$GOPATH` environment variable, which had limitations. It was challenging to handle different dependency versions for different projects and ensure consistency across environments.
		- With Go modules, each project has its own independent module management. Dependencies are defined in a `go.mod` file, specifying versions or version ranges. Go modules automatically fetch the required dependencies when building the project.
		- Go modules improve reproducibility and portability, making it easier to share and collaborate on Go projects. They are the recommended approach for managing dependencies in Go.
	- ## Go Module Structure
		- Go modules are structured in a way that makes it easy to find and use the code they contain. The basic structure of a Go module is as follows
			- ```
			  module <module-path>
			  
			  require <dependency-module-path> <dependency-version>
			  
			  package <package-name>
			  ```
		- The `module-path` is the unique identifier for the module. It is a path that starts with a domain name or organization name, followed by a period, and then the name of the module. For example, the module path for the Go standard library is `golang.org/x/stdlib`.
		- The `require` directive specifies the dependencies of the module. The `dependency-module-path` is the path of the dependency module, and the `dependency-version` is the version of the dependency module that the current module requires.
		- The `package` directive specifies the name of the package that contains the code for the module.
		- In addition to these basic files, a Go module may also contain the following files:
			- `go.mod`: This file contains the module's metadata, such as its path, dependencies, and version.
			- `go.sum`: This file contains the checksums of the dependencies of the module.
			- `README.md`: This file is a human-readable description of the module.
		- The structure of a Go module makes it easy to find and use the code it contains. The `module-path` uniquely identifies the module, and the `require` directive specifies the dependencies of the module. This makes it easy to find the code that the module needs to run.
		- The `package` directive specifies the name of the package that contains the code for the module. This makes it easy to find the code that is relevant to the module.
		- The other files in a Go module are optional, but they can be helpful for understanding the module and how to use it.
	- ## Go Module Resources
		- [Using Go Modules - The Go Programming Language](https://go.dev/blog/using-go-modules)
		- [Go Modules Reference - The Go Programming Language](https://go.dev/ref/mod)
		- [How to Use Go Modules  | DigitalOcean](https://www.digitalocean.com/community/tutorials/how-to-use-go-modules)