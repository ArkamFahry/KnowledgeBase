tags:: [[PostgreSQL]]

- # PostgreSQL LISTEN and NOTIFY
	- PostgreSQL, `LISTEN` and `NOTIFY` are features used for asynchronous communication between database sessions, allowing real-time notification of events occurring within the database.
	- **LISTEN**
		- This command allows a database session to subscribe to notifications. When a session issues a `LISTEN` command for a particular channel, it waits for notifications on that channel.
	- **NOTIFY**
		- This command sends a notification to all sessions that are listening on a specific channel. When a `NOTIFY` command is executed for a certain channel, all sessions that have previously issued a `LISTEN` command for that channel will receive the notification.
	- How `LISTEN` and `NOTIFY` works
		- **Session A**
			- executes `LISTEN channel_name;`
		- **Session B**
			- inserts or updates data in the database and then executes: `NOTIFY channel_name, 'payload';`
		- **Session A**
			- receives a notification with the payload `'payload'` on `channel_name`.
	- This mechanism is often used in scenarios where real-time communication or updates are required between different parts of an application or between different users connected to the database. It's commonly used in conjunction with other programming languages or frameworks to create responsive applications that react to database changes in real-time.