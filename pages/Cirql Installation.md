tags:: [[Cirql]]

- # Cirql Installation
	- ## Cirql Install
	  id:: 649c425a-3f87-4002-81f6-6acdd51f00c8
		- [[Cirql]] query builder package can be installed from npm, together with a supported version of [[Zod]].
			- ```npm
			  npm install cirql zod
			  ```
		- Any other package manager cna also be used (npm, yarn, pnpm, etc).
	- ## Cirql Connection Setup
		- There are two types of available connections  stateful and stateless
		- ### Stateful Connection Setup
			- This will create a high performance Stateful WebSocket connection to [[SurrealDB WebSocket]] which will allows for easy bi-directional communication.
			- This allows you to maintain a single connection for all queries making it efficient but not suitable for Serverless environments.
			- ```typescript
			  import { Cirql } from 'cirql';
			  
			  const cirql = new Cirql({
			      connection: {
			          endpoint: 'http://localhost:8000/',
			          namespace: 'test',
			          database: 'test',
			      },
			      credentials: {
			          user: 'root',
			          pass: 'root',
			      }
			  });
			  ```
			- This will automatically make  Cirql open a WebSocket connection to [[SurrealDB]]. If the preference is to handle this manually, the configuration `autoConnect` needs to be set to `false`.
			- #### Waiting for the connection
				- Wait for the connection to open by using the ready function. From this point on you will be able to send queries to the database.
					- ```typescript
					  await cirql.ready();
					  ```
				- Alternatively, listen to the `open` event using `addEventListener`.
			- #### Manual connection management
				- If `autoConnect: false` this means it is disabled, the connection should be initiated using the connect function.
					- ```typescript
					  cirql.connect();
					  ```
				- When the connection is no longer required. The  connection can be dispose by simply calling the disconnect function.
					- ```typescript
					  cirql.disconnect();
					  ```
		- ### Stateless Connection Setup
			- The default connection method to [[SurrealDB]] using [[Cirql]] is [[WebSocket]] which are extremally performant. This allows the application to send queries to the database and receive the results in real-time. However, this means that the connection needs to be kept open. If the application is intended to run on a Serverless environment this will no be ideal.
			- In this scenario [[Cirql]] will use the [[HTTP]] to communicate with the [[SurrealDB HTTP]] endpoint which is stateless and doesn't need an open connection all the time. Connection's can be created and disposed for each request.
			- ```typescript
			  import { CirqlStateless, select } from 'cirql';
			  
			  const cirql = new CirqlStateless({
			      connection: {
			          endpoint: 'http://localhost:8000/',
			          namespace: 'test',
			          database: 'test',
			      },
			      credentials: {
			          user: 'root',
			          pass: 'root',
			      }
			  });
			  
			  // You can now use the cirql instance as normal without
			  // having to call .disconnect()
			  
			  const organisations = await cirql.execute({ 
			      query: select().from('organisation').where({ isEnabled: true }),
			      schema: Organisation
			  });
			  ```
			- Since there is no need to close a connection so there is need to keep a reference to the Cirql instance. For each request simply create a new instance.
			- When there is no need for stateless behavior is it highly recommended to use the stateful API instead. This will decrease the time each query takes as it doesn't need to authenticate for each request.
			  background-color:: yellow