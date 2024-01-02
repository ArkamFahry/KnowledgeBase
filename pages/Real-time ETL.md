tags:: [[ETL]]

- # Real-time ETL
	- Real-time ETL (Extract, Transform, Load) is a variation of traditional ETL processes designed to handle data in near real-time or with minimal latency. Unlike traditional batch-oriented ETL, where data is collected, processed, and loaded periodically in predefined intervals (such as nightly or weekly batches), real-time ETL deals with data as it becomes available, allowing for faster and more immediate processing and analysis.
	- ## How Real-time ETL works
		- **Extract**
			- Data is continuously or frequently extracted from various sources, such as databases, sensors, streams, APIs, or other systems, as soon as new information is generated or updated.
		- **Transform**
			- Upon extraction, data is immediately transformed or processed in real-time. Transformations may include cleansing, validation, enrichment, and other operations required to make the data usable for analysis or loading.
		- **Load**
			- Transformed data is then loaded into the target destination or database in near real-time. This destination could be a data warehouse, analytics platform, or any storage system used for immediate analysis or reporting.
	- Real-time ETL is commonly used in scenarios where up-to-date information is crucial for decision-making, such as in financial services (stock trading), monitoring systems (IoT sensors). It enables businesses to react swiftly to changing conditions and make informed decisions based on the most current data available.