# GoEmbed Directive
	- The [[Go]] embed directive to embed arbitrary files and folders into the [[Go Binary]] makes it convenient to add required assets and ship a single binary with no dependencies.
	- ## Embed Directive Use Cases
		- Embedding a web application
			- Like a web application. [[PocketBase]] has done this to ship a single binary with a admin ui
		- Embedding [[Database Migration]]. All the migrations files can be embedded into the binary so it doesn't need a external migration runner.
	- ## Process of Embedding
		- ### Import the `embed`
			- ```go
			  import (
			  	"embed"
			  )
			  ```
		- ### The embed directive
			- ```go
			  //go:embed
			  ```
		- ### Using the directive to embed a single file
			- ```go
			  //go:embed folder/single_file.txt
			  var fileString string
			  ```
			- ```go
			  	
			  //go:embed folder/single_file.txt
			  var fileByte []byte
			  ```
		- ### Using to embed multiple files or whole folders
			- For this the `embed.FS` comes in handy
				- This implements a simple virtual file system that holds all the required files and folders.
			- ```go
			  //go:embed folder/single_file.txt
			  //go:embed folder/*.hash
			  var folder embed.FS
			  ```
		- ### The combination of all the above
			- ```go
			  package main
			  
			  import (
			      "embed"
			  )
			  
			  //go:embed folder/single_file.txt
			  var fileString string
			  
			  //go:embed folder/single_file.txt
			  var fileByte []byte
			  
			  //go:embed folder/single_file.txt
			  //go:embed folder/*.hash
			  var folder embed.FS
			  
			  func main() {
			  
			      print(fileString)
			      print(string(fileByte))
			  
			      content1, _ := folder.ReadFile("folder/file1.hash")
			      print(string(content1))
			      content2, _ := folder.ReadFile("folder/file2.hash")
			      print(string(content2))
			  }
			  ```
	- ## Important Note
	  background-color:: yellow
		- The files or folders need to be relative to the go file where the embed is happening
			- ```
			  project/
			  |-- main.go
			  |-- relative/
			  |   |-- path/
			  |   |   |-- to/
			  |   |   |   |-- file.txt
			  |   |   |-- folder/
			  |   |   |   |-- file1.txt
			  |   |   |   |-- file2.txt
			  |   |   |   +-- ...
			  ```
			- ```go
			  //go:embed relative/path/to/file.txt
			  var fileContent string
			  
			  //go:embed relative/path/to/folder/*
			  var folderContent embed.FS
			  ```
			- This path is relative is  required or the embedding will fail with errors like.
				- `Invalid Path`
					- If you provide an invalid or non-existent path in the `//go:embed` directive, Go will raise an error during the build.
				- `File Not Found`
					- If the file specified in the `//go:embed` directive does not exist at the provided relative path, Go will generate an error indicating that the file could not be found.
				- `Folder Not Found`
					- Similarly, if the folder specified in the `//go:embed` directive does not exist at the provided relative path, Go will generate an error indicating that the folder could not be found.
				- `Permission Denied`
					- In some cases, you might encounter a permission-related error if the Go compiler doesn't have the necessary permissions to access the files or folders during the build process.
					- This can happen if there are not enough privileges to read files.