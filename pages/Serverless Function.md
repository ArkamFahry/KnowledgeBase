tags:: [[Serverless]]

- # Serverless Function
	- Serverless functions, also known as Function-as-a-Service (FaaS), are a cloud computing execution model where a cloud provider dynamically manages the allocation of machine resources. In this setup, developers focus solely on writing and deploying code, without dealing with the underlying infrastructure like servers, operating systems, or scaling concerns.
	- ## Workings of serverless function
		- **Event-Driven Execution**
			- Serverless functions are triggered by specific events. These events could be HTTP requests, database changes, file uploads, or custom events within an application.
		- **Pay-Per-Use Pricing**
			- With serverless computing, you're billed based on the actual resources consumed by your functions rather than paying for a fixed amount of resources or server uptime.
		- **Scalability**
			- Serverless architectures automatically scale by spinning up instances of the function as needed in response to incoming requests. This enables handling varying workloads without manual intervention.
		- **Statelessness**
			- Functions are typically stateless, meaning they don't retain information between invocations. Any required data persistence usually involves external services like databases or storage.
		- **Ease of Deployment**
			- Developers can easily deploy functions through the cloud provider's interface or via command-line tools. This rapid deployment facilitates quick iteration and updates.
		- **Supported Languages*
			- * Most serverless platforms support multiple programming languages, allowing developers to use their preferred language for writing functions.
	- Popular serverless platforms include [[AWS Lambda]] , [[Azure Function]], [[GCP Cloud Function]], and more. These services offer a wide range of triggers and integrations, enabling developers to build highly scalable and event-driven applications without worrying about the underlying infrastructure's management.
	- Serverless doesn't mean "no servers"; rather, it abstracts the server management from developers, allowing them to focus on writing code and delivering value while the cloud provider takes care of the underlying infrastructure.