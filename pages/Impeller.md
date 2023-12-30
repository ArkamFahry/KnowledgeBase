tags:: [[Flutter]]

- # Impeller: Flutter's New Rendering Engine
	- Impeller is a new rendering runtime for [[Flutter]]. It provides a solution to Flutter’s early-onset jank issue. Impeller precompiles a smaller, simpler set of shaders at Engine build time so they don’t compile at runtime. This leads to improved performance and smoother user experience.
	- ## Key features of Impeller
		- **Predictable Performance**
			- Impeller compiles all shaders and reflection offline at build time. It builds all pipeline state objects upfront. The engine controls caching and caches explicitly.
		- **Instrumentable**
			- Impeller tags and labels all graphics resources like textures, and buffers. It can capture and persist animations to disk without affecting per-frame rendering performance.
		- **Portable**
			- Flutter doesn’t tie Impeller to a specific client rendering API. You can author shaders once and convert them to backend-specific formats as necessary.
		- **Leverages Modern Graphics APIs**
			- Impeller uses, but doesn’t depend on, features available in modern APIs like Metal and Vulkan.
		- **Leverages Concurrency**
			- Impeller can distribute single-frame workloads across multiple threads if necessary.
	- Impeller is enabled by default on iOS and is available for macOS in preview. As of Flutter 3.16, Impeller is available behind a flag on Android devices that support Vulkan. This new rendering engine is part of Flutter’s continuous effort to improve performance and provide a smooth user experience.