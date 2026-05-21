# Implementing Indexing Phase of RAG

Is slide mein hum RAG ka indexing phase code ke though implement karenge.

Indexing Phase:
- Load the documents.
- Divide the documents in chunks.
- Create the Embedding of chunks.
- Store the Embedding in Vector DB.

Ye Indexing phase ke steps hote hain.

<br>

Make sure ki ```Qdrant``` DB running ho.

### Running Qdrant DB Locally using Docker

```docker-compose.yaml```
```
version: '3.8'

services:
  vector-db:
    image: qdrant/qdrant:latest
    container_name: vector-db
    ports:
      - "6333:6333"
```

Run:
```
docker-compose up -d
```
Qdrant db port ```http://localhost:6333/``` par run hoga

<br>
<br>

### Step-1: Implementing Load the Documents step of Indexing Phase

**Installing the necessary Libraries**
```
pip install langchain-community
pip install pypdf
```

**Create a directory structure and files in it**:
```
/Implementing RAG
    |- index.py
    |- Mastering_Azure_Cloud.pdf
```

<br>

```index.py```: This file is loading a pdf file into python program and printing in a page.
```
from pathlib import Path
from langchain_community.document_loaders import PyPDFLoader

pdf_path = Path(__file__).parent / "Mastering_Azure_Cloud.pdf"


# Load the file in python program

loader = PyPDFLoader(file_path=pdf_path)

pages = loader.load() # This load method is loading the pdf into pages. We can print page by page.

print(pages[1])
```
loader pdf ko page by page load karta hai. Hum page number dekar particular page ko print karwa sakte hain.

Output:
```
page_content='Azure Portal
Azure provides 3 administration tools to choose from1. The Azure Portal2. The Azure CLI3. Azure PowerShell
● We canusetheAzure GUIportalwebsite(portal.azure.com)tocreate,configure,andalter our Azure subscription resources.● We canlocate theresourceneededandexecute any changes.We have wizardsandtooltips to guide through various administrative tasks.● Pleasenote that we cannotusetheportalto performrepetitive tasks like creating12VMs etc.● Weneedtouseothertoolstoavoiderrors,anditwillalsobeatime-consumingprocessto do on the portal.
The Azure portal can be divided into 3 sections.
1. Left — A list of resources and services to createand manage your Azure environment.2. Center —Adashboardthatyoucantailortomeetyour(PublicorPrivatedashboards)needs.3. Top —Asearchbartoquicklyfindresourcesandservices,anotificationicon,accessto a web-based command line, and more.
● Let’s try to create a resourceandseehow to usethePortal.Forexample,let us ● ClickontheBurgermenuonthelefttopandselectResourcegroupandclickonit.You will get a new Panel.
--Back to Index-- 2
create a resource group called demystify.' metadata={'producer': 'PyPDF', 'creator': 'PyPDF', 'creationdate': '', 'source': 'C:\\Users\\puneetverma02\\OneDrive - Nagarro\\Desktop\\Puneet_DevOPs\\6 - Generative and Agentic AI with python\\7 - Implementing RAG\\Mastering_Azure_Cloud.pdf', 'total_pages': 104, 'page': 1, 'page_label': '2'}
```

<br>
<br>

### Step-2: Dividing the ducoment in Chunks

To uper wale step se humne document ko page by page python code mein load kiya.

Ab is step mein hum document ko chunks mein divide karenge. Chunk mein divide karne ke liye langchain ki ```langchain-text-splitters``` library ka use kiya jata hai.

**Install Python LangChain Library**:
```
pip install -U langchain-text-splitters
```

<br>

Complete Python Code:
```
from pathlib import Path
from langchain_community.document_loaders import PyPDFLoader
from langchain_text_splitters import RecursiveCharacterTextSplitter

pdf_path = Path(__file__).parent / "Mastering_Azure_Cloud.pdf"


# Load the file in python program

loader = PyPDFLoader(file_path=pdf_path)

docs = loader.load()


# Split the loaded file into smaller chunks

text_splitter = RecursiveCharacterTextSplitter(chunk_size=1000, chunk_overlap=400)

splits = text_splitter.split_documents(document=docs)
```

<br>
<br>

### Step-3: Create the Vector Embeddings of Chunks and store into vector db

Uper wale step mein humne document ko chunks mein divide kiya. Lekin is step mein hum chunks ki vector embeddings create karenge aur usko vector db mein store karenge.

Iske liye ye **python library install karenge**:
```
pip install langchain-google-genai
pip install langchain-qdrant
```

Mai is code ke liye Google AI Studio ki Api Key use kar rha hua. Code ko yahan commit karne se pehle maine actual API Key ko "My_API_Key " se replace kar diya hai kyuki yahan commit karne se api key expose ho rhi thi jo ki best practise nahi hai.

<br>

Python code using Udemy course
```
# from pathlib import Path
# from langchain_community.document_loaders import PyPDFLoader
# from langchain_text_splitters import RecursiveCharacterTextSplitter
# from langchain_google_genai import GoogleGenerativeAIEmbeddings
# from langchain_qdrant import QdrantVectorStore
# from dotenv import load_dotenv

# load_dotenv()

# pdf_path = Path(__file__).parent / "Mastering_Azure_Cloud.pdf"


# # Load the file in python program

# loader = PyPDFLoader(file_path=pdf_path)

# docs = loader.load()


# # Split the loaded file into smaller chunks

# text_splitter = RecursiveCharacterTextSplitter(chunk_size=1000, chunk_overlap=100)

# chunks = text_splitter.split_documents(documents=docs)

# # print(chunks[1].page_content)  # Print the first chunk to verify the content


# # Create the embeddings for the chunks

# embeddings_model = GoogleGenerativeAIEmbeddings(model="models/gemini-embedding-001", google_api_key="MY_API_KEY")

# vector_store = QdrantVectorStore.from_documents(documents=chunks, embedding=embeddings_model, url = "http://localhost:6333", collection_name="learning_rag", batch_size=32)

# print("Indexing Phase complete!")
```

Phle maine ye code likha tha kyuki mai google ai studio ki free api use kar rha the to rate limiting ka error aa rha tha, issue bachne ke liye maine gemini se ye code generate karwaya, jisme gemini ne 20 seconds ka gap ke baad chunks ki vector embedding bana ke docker mein chal rhae qdrant db mein embedding store ki.

Agar api key banani hai to aap Google AI Studio se API key bana sakte hain.

Complete python code:
```
import os
import time
from pathlib import Path
from dotenv import load_dotenv
from langchain_community.document_loaders import PyPDFLoader
from langchain_google_genai import GoogleGenerativeAIEmbeddings
from langchain_qdrant import QdrantVectorStore
from langchain_text_splitters import RecursiveCharacterTextSplitter
from qdrant_client import QdrantClient
from qdrant_client.models import Distance, VectorParams

load_dotenv()

pdf_path = Path(__file__).parent / "Mastering_Azure_Cloud.pdf"

# 1. Load the file
loader = PyPDFLoader(file_path=pdf_path)
docs = loader.load()

# 2. Split into chunks
text_splitter = RecursiveCharacterTextSplitter(chunk_size=1000, chunk_overlap=100)
chunks = text_splitter.split_documents(documents=docs)

# 3. Initialize Embedding Model
embeddings_model = GoogleGenerativeAIEmbeddings(
    model="models/gemini-embedding-001", google_api_key="MY_API_KEY"
)

# 4. Initialize Local Qdrant Client & Create Collection Manually
url = "http://localhost:6333"
collection_name = "learning_rag"
client = QdrantClient(url=url)

# Agar collection nahi bana, toh Gemini ke size (768) ke mutabik banayein
if not client.collection_exists(collection_name=collection_name):
    client.create_collection(
        collection_name=collection_name,
        vectors_config=VectorParams(size=768, distance=Distance.COSINE),
    )

# LangChain Vector Store Empty Instance
vector_store = QdrantVectorStore(
    client=client, collection_name=collection_name, embedding=embeddings_model
)

# 5. Safe Batching with Time Delay (Rate limit se bachne ke liye)
batch_size = 32
print(f"Total chunks: {len(chunks)}. Indexing shuru ho rahi hai...")

for i in range(0, len(chunks), batch_size):
    batch = chunks[i : i + batch_size]

    # Batch ko database mein add karein
    vector_store.add_documents(batch)
    print(f"Uploaded chunks {i} to {min(i + batch_size, len(chunks))}")

    # Agar aage aur batches hain, toh 15-20 seconds ka break lein taaki API reset ho sake
    if i + batch_size < len(chunks):
        print(
            "Rate limit (429) se bachne ke liye 20 seconds ka wait kar rahe hain..."
        )
        time.sleep(20)

print("Indexing Phase complete!")
```

Output:
```
Total chunks: 182. Indexing shuru ho rahi hai...
Uploaded chunks 0 to 32
Rate limit (429) se bachne ke liye 20 seconds ka wait kar rahe hain...
Uploaded chunks 32 to 64
Rate limit (429) se bachne ke liye 20 seconds ka wait kar rahe hain...
Uploaded chunks 64 to 96
Rate limit (429) se bachne ke liye 20 seconds ka wait kar rahe hain...
Uploaded chunks 96 to 128
Rate limit (429) se bachne ke liye 20 seconds ka wait kar rahe hain...
Uploaded chunks 128 to 160
Rate limit (429) se bachne ke liye 20 seconds ka wait kar rahe hain...
Uploaded chunks 160 to 182
Indexing Phase complete!
```

Yahan tak humne indexing phase complete kar liya hai.

