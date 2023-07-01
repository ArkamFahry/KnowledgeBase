- # Presence
  id:: 64a03c07-0ec8-4792-a6bb-354b43173185
	- Presence can be used to share state between clients. Each client maintains their own piece of state within the shared state.
	- Presence utilizes an in-memory conflict-free replicated data type ([[CRDT]]) to track and synchronize shared state in an eventually consistent manner. It computes the difference between existing state and new state changes and sends the necessary updates to clients via Broadcast.
	- When a new client subscribes to a channel, it will immediately receive the channel's latest state in a single message instead of waiting for all other clients to send their individual states.
	- Clients are free to come-and-go as they please, and as long as they are all subscribed to the same channel then they will all have the same Presence state as each other.
	- The neat thing about Presence is that if a client is suddenly disconnected (for example, they go offline), their state will be automatically removed from the shared state. If you've ever tried to build an “I'm online” feature which handles unexpected disconnects, you'll appreciate how useful this is.
	- ## Presence Resources
		- [Presence | Supabase Docs](https://supabase.com/docs/guides/realtime/presence)