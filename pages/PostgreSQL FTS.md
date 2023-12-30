tags:: [[PostgreSQL]]

- # PostgreSQL FTS: PostgreSQL Full-Text Search
	- PostgreSQL Full Text Search (FTS) is a powerful feature that allows you to perform text-based searching in a [[PostgreSQL]] database efficiently. It enables complex text searching operations by creating indexes on text data, making the searches faster and more effective than traditional `LIKE` or `ILIKE` queries.
	- ## Key features of PostgreSQL Full Text Search include
		- Text Search Configurations
			- PostgreSQL supports multiple text search configurations, each with its own set of rules for text processing. These configurations can handle different languages, stemming, stopword removal, and other language-specific requirements.
		- Text Search Indexes
			- To perform fast and efficient full-text searches, PostgreSQL allows you to create specialized indexes using the `tsvector` data type. These indexes store a preprocessed and weighted representation of the text content, enabling quick searches for words and phrases.
		- Text Search Functions
			- PostgreSQL provides several built-in functions for text search, such as `to_tsvector`, `to_tsquery`, and `ts_rank`, which allow you to convert text into `tsvector`, perform text query transformations, and rank search results based on relevance.
		- Ranking
			- Full-Text Search in PostgreSQL allows ranking search results based on relevance. The `ts_rank` function allows you to sort the results based on their text match quality, making it easier to present the most relevant results to users.
		- Morphological Processing
			- PostgreSQL's Full-Text Search supports morphological processing, which means that words with different forms (e.g., plural/singular or verb tenses) can be matched during searches. This is achieved through stemming algorithms that normalize words to their base form.
		- Stopwords
			- Stopwords are common words that are often excluded from search queries because they don't add significant meaning to the search. PostgreSQL allows you to define custom stopword lists to improve search performance.
		- Phrase Search
			- With Full-Text Search, you can perform phrase searches, which means finding occurrences of specific phrases or word combinations within the text content.
	- ## To use Full-Text Search in PostgreSQL,  follow these steps
		- Enable Full-Text Search
			- PostgreSQL has Full-Text Search capabilities enabled by default. However, if you are using an older version or a custom build, you may need to ensure that the `pg_trgm` extension and necessary text search dictionaries are available.
		- Define Text Search Configurations
			- Create or select a text search configuration that matches your language and requirements. PostgreSQL provides a default configuration for English (`english`), but you can create custom configurations to suit other languages or specific search needs.
		- Create a Full Text Search Index
			- Define a `tsvector` column in your table to store the preprocessed and indexed text data. Then, create a Full-Text Search index on this column using the selected text search configuration.
		- Perform Full Text Searches
			- To perform Full-Text Searches, use the `MATCH` or `@@` operator in your SQL queries along with the `to_tsquery` function to convert the search query into a tsquery. This allows you to find matching rows in the table.
	- ## Examples for FTS
		- Create a simple table named `movies` to store movie data, and then we'll enable Full-Text Search on the `title` and `description` columns. We'll use PostgreSQL's Full-Text Search capabilities to allow users to search for movies based on their titles and descriptions. For this example, we'll use the default `english` text search configuration.
			- Create the `movies` table
				- ```sql
				  CREATE TABLE movies (
				  	id SERIAL PRIMARY KEY,
				  	title VARCHAR(100),
				  	description TEXT
				  );
				  ```
			- Enable Full-Text Search
				- ```sql
				  -- Enable the 'pg_trgm' extension (only if it's not already enabled)
				  CREATE EXTENSION IF NOT EXISTS pg_trgm;
				  -- Create the Full Text Search index on 'title' column
				  CREATE INDEX idx_fts_title ON movies USING GIN(to_tsvector('english', title));
				  -- Create the Full Text Search index on 'description' column
				  CREATE INDEX idx_fts_description ON movies USING GIN(to_tsvector('english', description));
				  ```
			- Insert some movie data
				- ```sql
				  INSERT INTO movies (title, description) VALUES
				    ('The Shawshank Redemption', 'Two imprisoned men bond over several years, finding solace and eventual redemption through acts of common decency.'),
				    ('The Godfather', 'The aging patriarch of an organized crime dynasty transfers control of his clandestine empire to his reluctant son.'),
				    ('Inception', 'A thief who steals corporate secrets through the use of dream-sharing technology is given the inverse task of planting an idea into the mind of a C.E.O.'),
				    ('Interstellar', 'A team of explorers travel through a wormhole in space in an attempt to ensure humanity\'s survival.');
				  ```
			- Perform Full-Text Search
				- Now, search the movies based on their titles and descriptions using Full-Text Search. Here's an example of how you can search for movies that match a specific query
					- ```sql
					  -- Search for movies with 'redemption' in the title or description
					  SELECT * FROM movies WHERE to_tsvector('english', title || ' ' || description) @@ to_tsquery('english', 'redemption');
					  -- Search for movies with 'dream' in the title or description
					  SELECT * FROM movies WHERE to_tsvector('english', title || ' ' || description) @@ to_tsquery('english', 'dream');
					  -- Search for movies with 'crime' in the title or description
					  SELECT * FROM movies WHERE to_tsvector('english', title || ' ' || description) @@ to_tsquery('english', 'crime');
					  ```
				- In this example, we concatenate the `title` and `description` columns in the `to_tsvector` function so that the search considers both fields for each movie.
		- Please note that this is a basic example to demonstrate the usage of Full Text Search in PostgreSQL. In a real-world scenario, you may need to handle various factors like stemming, stopword removal, and relevance ranking based on your specific use case. If it's a highly complex search scenario bring in a [[Search Engine]] like [[Elasticsearch]], [[OpenSearch]], [[Meilisearch]], [[Typesense]], [[ZincSearch]] or [[Algolia]].
- The actual implementation might vary depending on your specific use case, indexing requirements, and data size. Full-Text Search is a powerful tool to enhance text-based searching in your PostgreSQL database and is particularly useful for applications like content management systems, search engines, and product catalogs.