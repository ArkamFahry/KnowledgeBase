tags:: [[Supabase]], [[Elixir]], [[WebSockets]], [[Realtime Database]]

- # Supabase Realtime: Send ephemeral messages, track and synchronize shared state, and listen to Postgres changes all over WebSockets
	- ## Supabase Realtime
		- Simply put this is Server built built with [[Elixir]] using the [[Phoenix Framework]] that enables the following functionality.
			- [[Supabase Realtime Broadcast]]
				- Send ephemeral messages from client to clients with low latency.
			- [[Supabase Realtime Presence]]
				- Track and synchronize shared state between clients.
			- [[Supabase Realtime Postgres Changes]]
				- Listen to Postgres database changes and send them to authorized clients.
		- The server does not guarantee that every message will be delivered to clients so keep this in mind when using Realtime.
	- ## Channel
		- A channel is the basic building block of Realtime and narrows the scope of data flow to subscribed clients. You can think of a channel as a chatroom where participants are able to see who's online and send and receive messages; similar to a Discord or Slack channel.
		- All clients can connect to a channel and take advantage of the built-in features, Broadcast and Presence, while extensions, like Postgres Changes, must be enabled prior to use.
	- ## Supabase Realtime Resources
		- [Realtime | Supabase Docs](https://supabase.com/docs/guides/realtime)
		- [GitHub - supabase/realtime: Broadcast, Presence, and Postgres Changes via WebSockets](https://github.com/supabase/realtime)