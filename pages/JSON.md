# JSON
	- JSON stands for JavaScript Object Notation. It's a lightweight, human-readable format used for transmitting and storing data. JSON is often used to send data between a server and a web application as a text file.
		- ## Some key aspects of JSON
			- **Format** JSON is built on two structures:
				- A collection of key/value pairs. In various programming languages, this is realized as an object, record, dictionary, hash table, etc.
				- An ordered list of values. This structure is often realized as an array, list, vector, or sequence.
			- **Syntax**
				- JSON data is written as key-value pairs separated by commas. Keys are always strings enclosed in double quotes, followed by a colon, and then the corresponding value. Values can be strings, numbers, arrays, objects, booleans, null, or nested combinations thereof.
				- ```json
				  {
				  	"name": "John Doe",
				  	"age": 30,
				  	"isStudent": false,
				  	"hobbies": ["reading", "coding", "hiking"],
				  	"address": {
				    		"street": "123 Main St",
				    		"city": "Anytown"
				  	}
				  }
				  ```
				- **Usage**
					- JSON is language-independent, making it easy to read and write for both humans and machines. It's commonly used in web development to transmit data between a server and a client (browser or mobile app). APIs often use JSON to format data sent and received during requests and responses.
				- **Popularity**
					- Its simplicity and ease of use have made JSON the preferred data interchange format for many web-based applications and [[API]]s.
			- JSON is widely supported in various programming languages with built-in functions to parse JSON strings into data structures native to that language and vice versa, making it a versatile and popular choice for data representation and exchange in modern applications.