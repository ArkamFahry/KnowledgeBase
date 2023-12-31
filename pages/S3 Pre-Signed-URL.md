tags:: [[Amazon S3]]

- # S3 Pre-Signed-URL
	- A pre-signed URL in [[Amazon S3]] is a way to grant temporary access to objects stored in an S3 bucket. Normally, accessing objects in an S3 bucket requires appropriate permissions set either through bucket policies or access control lists (ACLs). However, there are situations where you might want to provide time-limited access to a specific object without changing its permissions permanently.
	- This is where pre-signed URLs come in handy. They are URLs that grant limited permission to perform specific actions on an object in S3 for a predetermined period of time. These URLs are generated using your AWS credentials (access key and secret key) and are signed using cryptographic signatures.
	- ## How pre-signed URL's work
		- **Generate a pre-signed URL**
			- Using the AWS SDK or AWS CLI, you can generate a pre-signed URL for a specific object in your S3 bucket. You specify details like the HTTP method (GET, PUT, DELETE, etc.) and expiration time for the URL.
		- **Distribute the URL**
			- Once generated, this URL can be distributed to the intended users or applications. They can use this URL to perform the allowed action (like downloading an object via GET request or uploading via PUT request) on the specified S3 object.
		- **Time-limited access**
			- The pre-signed URL has a limited lifespan that you set during its creation. Once the expiration time is reached, the URL becomes invalid, and any attempts to use it will result in an error.
	- ## Pre-signed URLs advantages over providing direct access to resources
		- **Scalability and Performance** (Using Direct Upload to S3)
			- Pre-signed URLs allow you to offload the file transfer process directly to the client, enabling direct uploads to S3 without passing through your servers. This reduces the load on your infrastructure, improving scalability and performance.
		- **Limited Access Window**
			- Pre-signed URLs have an expiration time that you set. This time limit reduces the window of access to the resource, enhancing security by ensuring access is only available for a specific period.
		- **Fine-grained Control**
			- You can tailor permissions for specific operations (GET, PUT, DELETE) on individual objects using pre-signed URLs. This granularity allows you to control exactly what actions can be performed within the given timeframe.
		- **Avoiding Permanent Changes**
			- With pre-signed URLs, you don't need to permanently alter access permissions on your S3 bucket or objects. This is especially useful when you want to maintain strict access controls while temporarily allowing certain actions.
		- **Temporary Sharing**
			- It's useful for sharing resources securely for a limited time. Instead of granting ongoing permissions, you can provide temporary access to resources without needing to modify access policies.
		- **Secure Sharing Without Credentials**
			- Users or applications accessing the resources via pre-signed URLs don’t need AWS credentials. This reduces the risk of exposing long-term credentials and allows access without the need for explicit AWS authentication.
		- **Flexible Usage Scenarios**
			- Pre-signed URLs can be used in various scenarios, such as providing time-limited access to private content, enabling temporary uploads for unauthenticated users, or facilitating secure downloads for limited periods.
		- **Ease of Implementation**
			- They can be generated programmatically using AWS SDKs or AWS CLI, making it relatively straightforward to integrate and manage temporary access to S3 resources within your applications or systems.
		- **Efficient File Transfers**
			- By utilizing pre-signed URLs in combination with tools that support resumable downloads or chunked transfers, you can optimize bandwidth usage. Users can resume interrupted downloads without starting from scratch, which can save bandwidth.