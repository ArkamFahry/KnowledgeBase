tags:: [[Supabase Realtime]]

- # Broadcast
  id:: 64a032e1-1085-4f45-b7fd-c080f7e848ae
	- Realtime Broadcast follows the [[Pub]] where a client publishes messages to a channel based on a unique topic. For example, a user could send a message to a channel with topic `room-1`.
	- Other clients can receive the message in real-time by subscribing to the channel with topic `room-1`. These clients can continue to receive messages as long as they continue to be online and subscribed to the same channel topic.
	- An example use-case is sharing a user's cursor position with other clients in an online tool or game.
	- ## Broadcast Resources
		- [Broadcast | Supabase Docs](https://supabase.com/docs/guides/realtime/broadcast)