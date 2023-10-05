# SurrealDB Live Queries
	- ## SurrealDB Live Queries push data changes to the client's in realtime
		- In simple terms its just like [[Firebase/Realtime Database]] or [[Supabase/Realtime]] but with sql like syntax with more capability than any of them.
		- Live queries are so good any `select` statement can be turned into a live query by just making it a `live select`
			- Example normal `select`
				- ```sql
				  select * from users;
				  ```
			- Now lets turn it into a live query
				- There are two types of live select
				- Normal live select
					- ```sql
					  live select * from users;
					  ```
						- Now all the changes done to table like `create`, `update` and `delete` will be pushed to the subscribed client.
						- This will be the be the full record in case of `create`, `update` and in case of `delete` it will the record id of the deleted record.
				- Diff live select
					- ```sql
					  live select diff from users;
					  ```
						- This will also push changes to `create`, `update` and `delete` events to the subscribed client but it will not be the whole record it will be the change delta or only the change difference between the new record and old record.