tags:: [[BaaS]], [[GraphQL]], [[REST]], [[PostgREST]], [[PostgreSQL]], [[Realtime Database]]

- # Supabase: The Open Source Firebase Alternative
	- ![supabase.png](../assets/supabase_1687622345462_0.png)
	- ## Supabase
		- Supabase is a [[BaaS]] platform which radically simplify the process on back end development without the fear of [[Vendor lock-in]] because Supabase is completely base on [[Open Source]] software.
		- Put it simply Supabase is an opensource alternative to [[Firebase]] built with free and [[Open Source]] software.
	- ## Supabase Features
		- Admin Dashboard.
			- Supabase has a best in class admin dashboard called [[Supabase Studio]] which gives the user a clean and easy to use UI to interact with all the services in Supabase.
		- Full Managed Database.
			- There is fully managed [[PostgreSQL]] database loaded with a lot of  [[PostgreSQL Extensions]].
			- The database has full [[PostgreSQL Functions]] Support.
			- Complete support for [[PostgreSQL Triggers]].
			- Database [[Webhooks]] support built into the database.
			- Complete support for [[PostgreSQL FTS]] search.
			- Databse level secrets data encryption using extension [Supabase Vault](https://supabase.com/blog/supabase-vault).
			- Database migrations.
				- Develop locally and push your changes to your production database using migrations.
			- Managed daily database backups with option to upgrade to Point in Time recovery.
		- Multiple auth methods.
			- Email & Password Logins.
			- Magic Links.
			- Social Logins with multiple OAuth providers.
			- Phone Logins.
		- Authorization using [[PostgreSQL RLS]].
			- Control the data each user can access with [[PostgreSQL Policies]].
		- APIs & Client libraries for many different languages and environments.
		- Auto generated API's.
			- [[REST]]
				- Supabase automatically generates a REST API for the database using [[PostgREST]].
			- [[GraphQL]]
				- The GraphQL API implemented by Supabase runs and resolves its queries and mutations in the database layer using the extension [pg_graphql](https://supabase.github.io/pg_graphql/). This makes the GraphQL API extremely efficient and fast. In the meantime, this approach removes the dreaded [[GraphQL N + 1 Problem]].
		- [[Supabase Realtime]] which is cool
			- Supabase Realtime Database Changes will be pushed to the client via [[WebSockets]] in Realtime.
			  id:: 649f8cb9-6b54-4d1c-9481-9da89c4242e3
			- Supabase Broadcasting can be used to send messages between users through [[WebSockets]]. In this process, the database is bypassed and the messages are directly sent between clients, making Broadcasting much faster.
			- Supabase Presence Support.
				- Presence can be used to share the state between clients. Each client maintains their own piece of the state within the shared state. This is an extremely hard and complex thing to achieve which is a breeze to use in Supabase.
		- Storage with all the cool stuff
			- Supabase File Storage
				- A [[Object Storage]] system with a developer-friendly API to interact with.
			- Resumable uploads
				- The storage system also implements [[Tus]] of resumable file uploads to make large file uploads easy.
			- Storage CDN to cache large files on the edge.
			- Image Transformations on the fly.
				- Supabase Storage offers the functionality to transform and resize images dynamically. Any image stored in your buckets can be transformed and optimized for fast delivery.
		- Supabase Edge Functions
			- [[Deno]] based globally distributed [[TypeScript]] functions to execute custom business logic.
		- Project Management
			- Supabase CLI
				- CLI to develop your project locally and deploy to the Supabase Platform.
			- Supabase Management API
				- API to manage projects programmatically.
	- ## Supabase Problems
		- Relatively new service. Not enough time to cook in the oven.
		- In the hosted service there is no control over the underlying infrastructure.
		- Self Hosting Supabase can be a challenge because the multiple services required by Supabase to function are hard to deploy and manage.
		- The client SDKs are hard to migrate away from. Though Supabase uses standard [[PostgreSQL]] under the hood the Supabase clients are built to interact with the API which runs on top of the Database so migration would be a chalange.
		- If [[SQL]] is not the preferred way of data modelling  then Supabase is out the window.
		- The Authorization system is different. There needs to be a good level of understanding on [[PostgreSQL RLS]] to implement robust auth rules.
		- There is no offline data persistence in the SDKs.
	- ## Supabase Resources
		- [The Open Source Firebase Alternative | Supabase](https://supabase.com/)
		- [GitHub - supabase/supabase: The open source Firebase alternative. Follow to stay updated about our public Beta.](https://github.com/supabase/supabase)
		- [Supabase Docs](https://supabase.com/docs)
		- [Supabase - YouTube](https://www.youtube.com/c/supabase)
	- {{video https://www.youtube.com/watch?v=zBZgdTb-dns}}
	- {{video https://www.youtube.com/watch?v=WiwfiVdfRIc}}
	- {{video https://www.youtube.com/watch?v=VZUmIMBLV4I}}