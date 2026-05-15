# Local Vector DB Setup using Docker Compose

Pichle slide mein humne dekha ki RAG kya hota hai, kaise kaam karta hai aur kya kya components hote hain RAG ke ander.

To RAG mein 2 phases hote hain, 1 - Indexing Phase, 2 - Query Phase.

Indexing phase ke ander data ko chunks mein divide karke vector db mein store karte hain. To agar is phase ki implementation kare to sirf humko vector db hi setup karna padta hai.

To ab hum apne local system mein docker ke ander vector db ko setup karenge.

<br>

### Types of Vector DB

Market mein kaafi saare vector db hote hain, Jaise:
- **Pinecone**: A widely-used managed, serverless SaaS vector database ideal for production RAG pipelines due to its low-latency search and ease of use.
- **Weaviate**: An open-source, dedicated vector database with strong built-in vectorization modules and semantic search capabilities.
- **Qdrant**: Known for its performance, written in Rust, and offering efficient payload filtering for accurate retrieval.
- **Milvus**: Highly scalable, open-source database geared towards large-scale enterprise data with GPU acceleration.
- **Chroma**: A popular open-source, developer-friendly database, often used for local RAG implementations and ease of integration.
- **Redis**: Known for exceptionally fast speed, serving as both a primary database and a vector store.
- **pgvector**:  A cost-effective extension for PostgreSQL that enables vector storage within a familiar relational database environment.

<br>

To isme se **Qdrant** vector db light-weight hota hai aur fast hota hai. Aaj hum isi hi local system mein docker par setup karenge.

<br>
<br>

### Create a docker compose file

```docker-compose.yaml```:
```
version: '3.8'

services:
  vector-db:
    image: qdrant/qdrant:latest
    container_name: vector-db
    ports:
      - "6333:6333"
```

Start the container:
```
docker compose up -d
```

The vector db container will start on port 6333.
