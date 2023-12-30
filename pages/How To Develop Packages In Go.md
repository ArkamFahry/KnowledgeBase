tags:: [[Go]]

- # How To Develop Packages In Go: Building and Consuming Custom Packages
	- ## Package Development Prerequisites
		- [[Go]] needs to bee installed in the system.
	- ## Package Development
		- To create a new package, create a new directory for the project. In this case it's called `mypack`.
			- ```
			  mkdir mypack
			  ```
		- Next, navigate to the `mypack` directory and initialize it as a Go module.
			- ```
			  cd mypack
			  go mod init github.com/ArkamFahry/mypack
			  ```
			- This will create a `go.mod` file in the `mypack` directory.
		- Create a new file called `pack.go` in the directory `mypack`.
		  id:: 649d9f2f-ac9a-44d4-a1e6-b67bd38ba510
			- ```
			  touch pack.go
			  ```
		- Write the package code in `pack.go`.
			- ```go
			  package mypack
			  
			  import (
			   "fmt"
			  )
			  
			  func SayBagIsPacked() {
			    fmt.Println("The bag is packed")
			  }
			  ```
		- Building the Package in the directory `mypack`
			- ```
			  go build
			  ```
			- This will create a `mypack.a` file in the `mypack` directory.
	- ## Package Publishing
		- ### Connect to GitHub and Commit the Code
			- Create a new git repo as of this `github.com/ArkamFahry/mypack`
			- Initialize the Git repository and commit our changes.
				- ```git
				  git init
				  git add .
				  git commit -m "Initial commit"
				  ```
			- Add the remote origin for the repository.
				- ```git
				  git remote add origin https://github.com/ArkamFahry/mypack.git
				  ```
			- Finally, push the changes to the repository.
				- ```git
				  git push -u origin main
				  ```
		- ### Create a New Version
			- Tag the version using git for the usage of a specific versions.
				- ```git
				  git tag v0.0.1
				  ```
			- After version assigning, push this to the repository.
				- ```git
				  git push origin v0.0.1
				  ```
			- Now the package is published and ready to use.