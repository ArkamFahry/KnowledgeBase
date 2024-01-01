tags:: [[HTTP]]

- # HTTP streaming
	- HTTP streaming is a method of sending and receiving data over the web in a continuous stream, allowing content to be transmitted in small chunks rather than as a single large file. This enables a more seamless and real-time experience for users accessing multimedia content or other data online.
	- ## Types of HTTP streams
		- **Progressive Download**
			- Initially, the server sends the beginning portion of the file, allowing the client to start playing or viewing it while the rest of the file continues to download in the background. The file isn't played until it's fully downloaded.
		- **Adaptive Bitrate Streaming (ABR)**
			- This method adjusts the quality of the video or audio stream in real-time based on the user's internet speed and device capabilities. Popular protocols for ABR include MPEG-DASH (Dynamic Adaptive Streaming over HTTP) and HLS (HTTP Live Streaming).
		- **Chunked Transfer Encoding**
			- With this method, the server breaks the content into smaller chunks and sends them progressively. The client can start processing and displaying the received chunks without waiting for the entire file to download.
	- HTTP streaming is widely used in platforms like Netflix, YouTube, and other streaming services to deliver content efficiently while adapting to varying network conditions. It allows for smoother playback, reduced buffering, and a better user experience compared to traditional downloading methods.