# BSON
	- BSON stands for Binary [[JSON]]. It's a binary-encoded serialization format used primarily to store and exchange documents within databases, particularly in NoSQL databases like MongoDB.
	- ## Some key points about BSON:
		- **Binary Format**
			- BSON is a binary representation of JSON-like documents. While JSON is a text-based format, BSON represents the same information in a binary-encoded format, which makes it more efficient for storage and data exchange.
		- **Extended Data Types**
			- BSON extends the JSON data types by adding additional types such as Date and Binary Data. This extension allows for more precise representation of data, particularly in the context of databases where specific data types need to be maintained.
		- **Efficiency**
			- The binary encoding of BSON allows for more compact data representation compared to JSON, which can lead to more efficient storage and faster data retrieval.
		- **Rich Data Structures**
			- BSON supports various data types including strings, numbers, arrays, nested documents, boolean values, dates, binary data, regular expressions, and more. It retains the flexibility of JSON while accommodating additional types and features.
		- **Usage in Databases**
			- BSON is used as the primary data storage format in [[MongoDB]]. Documents stored in MongoDB are represented using BSON, enabling efficient storage, retrieval, and manipulation of data.
	- For instance, a JSON document might look like this
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
	- In BSON, this same document would be represented in a binary format, which is optimized for database storage and retrieval.
	- BSON's binary representation and support for additional data types make it well-suited for use in databases where efficiency, speed, and a wider range of data types are essential.