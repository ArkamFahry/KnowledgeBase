tags:: [[Go]]

- # Go Context
	- [[Go]] the `context` package provides a way to carry deadlines, cancellations, and other request-scoped values across API boundaries and between processes. It is commonly used in concurrent and distributed systems to manage the flow of cancellation signals, deadlines, and other request-specific data between different parts of an application.
	- The `context` package defines the `Context` type, which represents the context in which a particular operation is taking place. A `Context` can be created using the `context.Background()` function, and additional information can be associated with it using the `context.WithValue` function.
	- ## Key concepts related to Go's `context` package
		- **Background Context**
			- ```go
			   ctx := context.Background()
			   ```
				- This creates a root context. It is typically used as the starting point when creating other contexts.
		- **WithCancel**
			- ```go
			   ctx, cancel := context.WithCancel(parent)
			   ```
				- This creates a new context derived from the parent context (`parent`). The `cancel` function, when invoked, signals that the context and its children should be canceled.
		- **WithTimeout**
			- ```go
			   ctx, cancel := context.WithTimeout(parent, timeout)
			   ```
				- These create contexts with associated timeouts. If the timeout reached, the context is automatically canceled.
		- **WithDeadline**
			- ```go
			   ctx, cancel := context.WithDeadline(parent, deadline)
			   ```
				- These create contexts with associated deadlines. If the deadline reached, the context is automatically canceled.
		- **WithValue**
		   ```go
		   ctx := context.WithValue(parent, key, value)
		   ```
		   This creates a new context with an associated key-value pair. It's important to note that the values should be small and of types that don't change frequently, as they are intended for communication between different parts of the application.
	- 5. **Context Methods:**
	   The `Context` interface includes methods like `Deadline()`, `Done()`, and `Err()` that allow you to query information about the context.
	- Here's a simple example illustrating the use of a `context` with a timeout:
	- ```go
	  package main
	  - import (
	  "context"
	  "fmt"
	  "time"
	  )
	  - func main() {
	  // Create a context with a timeout of 2 seconds
	  ctx, cancel := context.WithTimeout(context.Background(), 2*time.Second)
	  defer cancel() // Cancel the context to release resources when done
	  - // Simulate some work that may take more than 2 seconds
	  go func() {
	  time.Sleep(3 * time.Second)
	  cancel() // Cancel the context after 3 seconds
	  }()
	  - select {
	  case <-ctx.Done():
	  fmt.Println("Operation canceled or timed out:", ctx.Err())
	  case <-time.After(4 * time.Second):
	  fmt.Println("Operation completed successfully")
	  }
	  }
	  ```
	- In this example, the program creates a context with a 2-second timeout. It then simulates a task that takes 3 seconds to complete. The select statement waits for either the context to be canceled or the 4-second timer to expire.
	- Using `context` helps manage the lifecycle of operations, especially in scenarios where you want to propagate cancellation signals or deadlines across different parts of your application.