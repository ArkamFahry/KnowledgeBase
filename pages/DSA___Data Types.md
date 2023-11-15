# Data Types
	- Variables are a term we all have herd in mathematics.
		- $$x^2 + 2y - 2 = 1$$
		- The above equation has name `x`, `y` which are variables. which have the ability to hold values. That means the names `x`, `y` are placeholders for representing data. Similarly, in computer science programming we need something for holding data, and variables is the way to do that.
	- As mentioned above.  `x` and `y` can take any values such as integral numbers (33, 69), real numbers (0.33, 69.69), or just 0 and 1. To solve the equation, we need to
	  relate them to the kind of values they can take. So in that case the kind of value they can take is called **Data Type** is the name used in computer science programming for this purpose.
	- A data type in a programming language is a set of data with predefined values. Examples of data types are: integer, floating point, unit number, character, string, etc.
	- Computer memory is all filled with zeros and ones. If we have a problem and we want to code it, it’s very difficult to provide the solution in terms of zeros and ones. To help users, programming languages and compilers provide us with data types. For example, integer takes 2 bytes (actual value depends on compiler), float takes 4 bytes, etc. This says that in memory we are combining 2 bytes (16 bits) and calling it an integer. Similarly, combining 4 bytes (32 bits) and calling it a float. A data type reduces the coding effort. At the top level, there are two types of data types.
		- System-defined data types (also called Primitive data types)
		- User-defined data types
	- ### System-defined data types (Primitive data types)
		- Data types that are defined by system are called primitive data types. The primitive data types provided by many programming languages are: int, float, char, double, bool, etc. The number of bits allocated for each primitive data type depends on the programming languages, the compiler and the operating system. For the same primitive data type, different languages may use different sizes. Depending on the size of the data types, the total available values (domain) will also change.
		  For example, int may take 2 bytes or 4 bytes. If it takes 2 bytes (16 bits), then the total possible values are -32,768 to +32,768 ($$-2^{15}$$ to $$2^{15}-1$$). If it takes 4 bytes (32 bits), then the possible values are between -2,147,483,648 and +2,147,483,647 ($$-2^{31}$$ to $$2^{31}-1$$). The same is the case for other data types.
	- ### User defined data types
		- to define their own data types, called user – defined data types. These are composed of primitive data types to build more domain specific data types. Good examples of user defined data types are: structures in [[C]], [[C + +]] ,[[Rust]] [[Go]]  or classes in [[C#]], [[Dart]], [[TypeScript]]
			- Let's create a user defined data type called `NewType`. This gives more flexibility and comfort in dealing with computer memory.
				- Structs
					- ```c
					  typedef struct {
					      char *Id;
					      char *Name;
					      char *Description;
					      long long CreatedAt;
					      long long UpdatedAt;
					  } NewType;
					  ```
					- ```c++
					  struct NewType {
					      std::string Id;
					      std::string Name;
					      std::string Description;
					      long long CreatedAt;
					      long long UpdatedAt;
					  };
					  ```
					- ```rust
					  struct NewType {
					      id: String,
					      name: String,
					      description: String,
					      created_at: i64,
					      updated_at: i64,
					  }
					  ```
					- ```go
					  type NewType struct {
					    Id string
					    Name string
					    Description string
					    CreatedAt int64
					    UpdatedAt int64
					  }
					  ```
				- Classes
					- ```c#
					  class NewType
					  {
					      public string Id { get; set; }
					      public string Name { get; set; }
					      public string Description { get; set; }
					      public long CreatedAt { get; set; }
					      public long UpdatedAt { get; set; }
					  }
					  ```
					- ```dart
					  class NewType {
					    String id;
					    String name;
					    String description;
					    int createdAt;
					    int updatedAt;
					  }
					  ```
					- ```ts
					  class NewType {
					    id: string;
					    name: string;
					    description: string;
					    createdAt: number;
					    updatedAt: number;
					  }
					  ```