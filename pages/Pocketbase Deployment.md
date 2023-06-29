- # PocketBase Deployment Methods
	- ## PocketBase Binary
		- Download the PocketBase binary for the specific platform
			- [Basics - Introduction - Docs - PocketBase](https://pocketbase.io/docs/)
		- Then run the below command to start the PocketBase binary
			- ```bash
			  ./pocketbase serve
			  ```
		- You could find all available commands and their options by running
			- ```bash
			  ./pocketbase --help or ./pocketbase [command] --help
			  ```
	- ## PocketBase Docker
		- ### Supported Architectures
			- Simply pulling `ghcr.io/muchobien/pocketbase:latest` should retrieve the correct image for your arch.
			- The architectures supported by this image are
				- |Architecture|Available|
				  |--|--|
				  |amd64|✅|
				  |arm64|✅|
				  |armv7|✅|
		- ### Version Tags
			- This image provides various versions that are available via tags. Please read the descriptions carefully and exercise caution when using unstable or development tags.
				- |Tag|Available|Description|
				  |---|---|---|
				  | latest|✅|Stable releases from PocketBase|
				  | x.x.x|✅|Patch release from PocketBase|
				  |x.x|✅|Minor release from PocketBase|
				  | x|✅|Major release from PocketBase|
		- ### Application Setup
			- Access the webui at `<your-ip>:8090`, for more information check out [PocketBase](https://pocketbase.io/docs/).
		- ### Usage
			- #### Docker Compose Yaml
				- ```yaml
				  version: "3.7"
				  services:
				    pocketbase:
				      image: ghcr.io/muchobien/pocketbase:latest
				      container_name: pocketbase
				      restart: unless-stopped
				      command:
				        - --encryptionEnv #optional
				        - ENCRYPTION #optional
				      environment:
				        ENCRYPTION: example #optional
				      ports:
				        - "8090:8090"
				      volumes:
				        - /path/to/data:/pb_data
				        - /path/to/public:/pb_public #optional
				      healthcheck: #optional (recommended) since v0.10.0
				        test: wget --no-verbose --tries=1 --spider http://localhost:8090/api/health || exit 1
				        interval: 5s
				        timeout: 5s
				        retries: 5
				  ```
			- #### Docker CLI
				- ```bash
				  docker run -d \
				    --name=pocketbase \
				    -p 8090:8090 \
				    -e ENCRYPTION=example `#optional` \
				    -v /path/to/data:/pb_data \
				    -v /path/to/public:/pb_public `#optional` \
				    --restart unless-stopped \
				    ghcr.io/muchobien/pocketbase:latest \
				    --encryptionEnv ENCRYPTION `#optional`
				  ```
	- ## PocketBase PocketHost
		- [Home - PocketHost](https://pockethost.io/)