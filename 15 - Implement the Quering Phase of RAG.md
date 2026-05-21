# Implementing the Quering Phase of RAG

Is slide mein hum RAG ke Quering Phase ko samjhenge aur code ke through implement karenge.

RAG system ka Querying Phase wo real-time process hota hai jo tab start hota hai jab user koi LLM se question puchta hai. Is phase mein system user ki query ko samajhta hai, us query ka embedding generate karta hai, fir vector database mein semantic similarity search perform karta hai taaki most relevant document chunks retrieve kiye ja sakein. Retrieved chunks ko original user query ke saath combine karke ek augmented prompt banaya jata hai, jo LLM ko diya jata hai. Fir LLM retrieved context ko use karke grounded, accurate aur context-aware answer generate karta hai. Simple words mein, Querying Phase ka main purpose hota hai user ke question ke according relevant knowledge dhoondhna aur us knowledge ki help se final intelligent response generate karna.

- User system ko question bhejta hai.
- User query ko vector/embedding mein convert kiya jata hai.
- Query embedding ko vector database mein compare kiya jata hai.
- Most semantically similar document chunks retrieve kiye jate hain.
- Top chunks ko combine karke final context banaya jata hai.
- Retrieved chunks + original query ko combine karke final prompt banaya jata hai.
- LLM prompt ko process karta hai aur documents se content find karke response generate karta hai.

<br>
<br>

### Create a Folder Structure
```
/Implementing RAG
    |- index.py
    |- Mastering_Azure_Cloud.pdf
    |- quering.py
```
Ye ```quering.py``` file mein hi code likhne wale hain.

<br>
<br>

### Python Code 

```quering.py```
```
rom langchain_google_genai import GoogleGenerativeAIEmbeddings
from langchain_qdrant import QdrantVectorStore
from openai import OpenAI

embeddings_model = GoogleGenerativeAIEmbeddings(
    model="models/gemini-embedding-001", google_api_key="AIzaSyDeoHCUgyTAZEYt9SZMQ-SXnnz4mhbO2B0"
)

vector_store = QdrantVectorStore.from_existing_collection(
    embedding=embeddings_model, 
    url="http://localhost:6333", 
    collection_name="learning_rag"
)

# Take the user input
user_query = input("Ask something about Azure Cloud: ")

# 1. Limit results to top 3 chunks
search_results = vector_store.similarity_search(query=user_query, k=3)

# Safe parsing for metadata keys
content_list = []
for results in search_results:
    page = results.metadata.get('page_label', results.metadata.get('page', 'Unknown'))
    source = results.metadata.get('source', 'Unknown')
    content_list.append(f"Page Content: {results.page_content}\nPage Number: {page}\nFile Location: {source}")

content = "\n\n\n".join(content_list)

# 2. Strict Prompting
SYSTEM_PROMPT = f"""
You are a strict AI assistant for answering questions related to Azure Cloud.

CRITICAL INSTRUCTIONS:
1. Answer the user's question ONLY using the provided Context below.
2. DO NOT use your own external knowledge or make assumptions.
3. If the answer is not explicitly mentioned in the Context, reply exactly with: "Mujhe iska jawab document mein nahi mila."
4. If you find the answer, provide the final response and at the very end of your answer, create a section called "Sources:" and list the Page Number and File Location used to answer the question.
5. Also draw diagrams if required to explain the answer better.

Context:
{content}
"""

client = OpenAI(
    api_key="AIzaSyDeoHCUgyTAZEYt9SZMQ-SXnnz4mhbO2B0",
    base_url="https://generativelanguage.googleapis.com/v1beta/openai/"
)

# 3. Added temperature=0.0
response = client.chat.completions.create(
    model="gemini-3-flash-preview", 
    messages=[
        {"role": "system", "content": SYSTEM_PROMPT},
        {"role": "user", "content": user_query}
    ],
    temperature=0.0 
)

print("\n--- Response ---")
print(response.choices[0].message.content)
```

Output:
```
Ask something about Azure Cloud: tell me about azure resource manager.

--- Response ---
Azure Resource Manager provides a management layer to create, update, and delete resources in your Azure account. It uses management features like access control, locks, and tags to secure and organize resources after deployment. When a user sends a request from any of the tools, APIs, or SDKs, the Resource Manager receives the request, authenticates/authorizes it, and then sends it to Azure services to take action. Since it acts as a central point, it leads to consistent results.

The benefits of Resource Manager include:
*   **Declarative templates:** You don't have to worry about the current state.
*   **Group deployments:** It allows for resources to be deployed as a group.
*   **Define dependencies:** Ensures the correct order of deployment.
*   **Apply tags:** Helps organize resources logically.
*   **Redeployment:** Provides confidence that the same results will be achieved upon redeployment.
*   **RBAC:** Applies access-control via Role-Based Access Control (RBAC) natively.

Sources:
Page Number: 9
File Location: C:\Users\puneetverma02\OneDrive - Nagarro\Desktop\Puneet_DevOPs\6 - Generative and Agentic AI with python\7 - Implementing RAG\Mastering_Azure_Cloud.pdf
```

<br>

Ye RAG complete ho chuka hai.
