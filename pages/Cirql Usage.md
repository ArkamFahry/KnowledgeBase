- ## Cirql Usage
	- ## Basic
		- Once [[Cirql Installation]] is completed and connected to SurrealDB, sending queries to the database can begin.
			- A simple `SELECT` statement raw query
				- ```typescript
				  import { query } from 'cirql';
				  
				  const profiles = await cirql.execute({ 
				      query: query('SELECT * FROM users WHERE age > $minAge'),
				      schema: z.any(),
				      params: {
				          minAge: 42
				      }
				  });
				  ```
				- The above example will send a raw string query to the database and return the result. The result will be validated against the provided schema, which in this case is `z.any()`. The minimum age is stored in a parameter, which will be automatically replaced in the query. Parameters are always escaped to prevent SQL injection attacks.
	- ## Query Writer API
		- Raw query strings is tedious and error prone. [[Cirql]] provides a Query Writer API to help to write queries in a more structured way.
		- ```typescript
		  import { select, RecordSchema } from 'cirql';
		  
		  export const Organisation = RecordSchema.extend({
		      name: z.string().min(1),
		      isEnabled: z.boolean(),
		      createdAt: z.string()
		  });
		  
		  const organisations = await cirql.execute({ 
		      query: select().from('organisation').where({ isEnabled: true }),
		      schema: Organisation // this is the typescript typing for the organization
		  });
		  ```
			- In the above example  `select` function is used to create the query writer. Any number of functions can chain to build up the required query. Cirql provides query writer functions for most common [[SurrealQL]] statements, likes of which are `update`, `delete`, `relate`, and many more.
			- The above example also makes use of a  [[Zod Schema]] to validate the query result. This schema is used to infer the TypeScript typing of the result. This means that the result is returned as if it was typed as `Organisation[]`. The schema property is required for all queries, however it can be set to `z.any()` to disable validation.
		- ### Available Query Writers
			- Currently provided Query Writers
				- `select()`
				- `count()`
				- `countRecord()`
				- `countRelation()`
				- `del()`
				- `delRecord()`
				- `delRelation()`
				- `create()`
				- `createRecord()`
				- `update()`
				- `updateRecord()`
				- `updateRelation()`
				- `relate()`
				- `relateRelation()`
				- `letValue()`
				- `query()`
	- ## Raw query values & operators
		- While the Query Writer API provides a safe way to write queries, it is still possible to insert raw values into the queries. This can be useful for inserting [[SurrealDB Functions]], operators or parameter names into `WHERE` clauses and `SET` expressions. By default values will use an equals sign (`=`) the `eq` expression.
		- In the belove example on creation of a new organization, and setting the `createdAt` field to the current time using the Surreal `time::now()` function.
			- ```typescript
			  import { time } from 'cirql'
			  
			  const profile = await cirql.execute({ 
			      query: create('organisation').setAll({
			          name: 'Example',
			          isEnabled: eq('$enable'),
			          createdAt: eq(time.now()) // time::now()
			      }),
			      schema: Organisation,
			      params: {
			          enable: true
			      }
			  });
			  ```
		- When adding or subtracting items from arrays,  The `add` and `remove` functions can be used instead of eq for inserting `+=` and `-=` operators.
		- ### Available raw functions
			- `rand`
			- `time`
			- `type`
	- ## Batched queries & transactions
		- While the can be `.execute()` used to send a single query to SurrealDB. The `.batch()` and `.transaction()` statement can be used to send multiple queries in a single request.
		- The returned array will contain the results of each query in the same order as they were sent. If [[TypeScript]] is used, the results will also be typed based on the schema that is provided. So the results can be destructured to get the individual values easily.
		- The below operation runs 4 queries in a single request and returns the values to an array of return value
			- ```typescript
			  const [a, b, c, d] = await database.batch(
			      {
			          query: create('organisation').setAll({
			              name: 'Example',
			              isEnabled: eq('$enable'),
			              createdAt: eq(timeNow())
			          }),
			          schema: Organisation,
			          params: {
			              enable: true
			          }
			      },
			      {
			          query: query('SELECT * FROM users WHERE age > $minAge').single(),
			          schema: Profile,
			          params: {
			              minAge: 42
			          }
			      },
			      {
			          query: count('organisation')
			      },
			      {
			          query: select('id').from('organisation').where({ isEnabled: true }),
			          schema: Organisation.pick({ id: true })
			      }
			  );
			  ```