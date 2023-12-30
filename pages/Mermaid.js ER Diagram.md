tags:: [[Mermaid.js]]

- # ER Diagrams
	- ```mermaid
	  erDiagram
	      CUSTOMER ||--o{ ORDER : places
	      ORDER ||--|{ LINE-ITEM : contains
	      CUSTOMER }|..|{ DELIVERY-ADDRESS : uses
	  ```