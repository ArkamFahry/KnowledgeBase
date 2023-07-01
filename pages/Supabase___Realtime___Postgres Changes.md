- # Postgres Changes
  id:: 64a03ba8-0162-4f7c-ba47-32bdf716f93f
	- Realtime's Postgres Changes feature listens for database changes and sends them to clients. Clients are required to subscribe with a JWT dictating which changes they are allowed to receive based on the database's [Row Level Security](https://supabase.com/docs/guides/auth/row-level-security).
	- Anyone with access to a valid JWT signed with the project's JWT secret is able to listen to your database's changes, unless tables have [Row Level Security](https://supabase.com/docs/guides/auth/row-level-security) enabled and policies in place.
	- Clients can choose to receive `INSERT`, `UPDATE`, `DELETE`, or `*` (all) changes for all changes in a schema, a table in a schema, or a column's value in a table. Your clients should only listen to tables in the `public` schema and you must first enable the tables you want your clients to listen to.
	- ## Postgres Change Resources
		- [Postgres Changes | Supabase Docs](https://supabase.com/docs/guides/realtime/postgres-changes)