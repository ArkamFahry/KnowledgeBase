- # Goroutines: Go Concurrency System
	- ## Goroutines
		- Go's concurrency system is based on goroutines and channels.
		- ### Goroutines
			- Goroutines are lightweight threads that are managed by the Go runtime. They are cheap to create and can be easily spawned from other goroutines.
		- ### Channels
			- Channels are a way for goroutines to communicate with each other. They can be used to send and receive data between goroutines, or to synchronize the execution of goroutines.
	- ## Simple Goroutines
		- A simple Goroutine
			- id:: 649eeca9-8c24-4598-ba0d-06561a9a64c2
			  ```go
			  func main() {
			    // Create a channel to communicate between goroutines.
			    ch := make(chan int)
			  
			    // Spawn a goroutine to print the numbers 1 to 10.
			    go func() {
			      for i := 1; i <= 10; i++ {
			        ch <- i
			      }
			    }()
			  
			    // Spawn a goroutine to print the numbers 11 to 20.
			    go func() {
			      for i := 11; i <= 20; i++ {
			        ch <- i
			      }
			    }()
			  
			    // Close the channel when all the numbers have been printed.
			    close(ch)
			  
			    // Wait for all the numbers to be printed.
			    for i := range ch {
			      fmt.Println(i)
			    }
			  }
			  ```
				- This program will spawn two goroutines, one to print the numbers 1 to 10 and the other to print the numbers 11 to 20. The goroutines will communicate with each other through the `ch` channel. The `main()` goroutine will wait for all the numbers to be printed before exiting.
	- ## Goroutine Features
		- Goroutines are lightweight
			- Goroutines are very lightweight, which means that they can be created and destroyed very quickly. This makes them ideal for concurrent programming, where you need to create a large number of small tasks.
		- Channels are a powerful way to communicate between goroutines
			- Channels provide a way for goroutines to send and receive data to each other. This is a very efficient way to communicate between goroutines, as it eliminates the need for locks and other synchronization primitives.
		- The Go runtime takes care of the scheduling of goroutines
			- The Go runtime is responsible for scheduling goroutines to run on the available CPU cores. This means that you don't have to worry about the details of scheduling, which can be a complex and error-prone task.