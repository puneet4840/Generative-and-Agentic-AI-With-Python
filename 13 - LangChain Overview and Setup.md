# LangChain Overview and Setup

Jab tum koi Agentic AI ya fir koi bhi AI related task karte ho. To tumko kaafi saari utilites ki jarurat hoti hai, Jaise:

For Example:
- Connecting to a vector database.
- Reading a document.
- Making some AI call

To ese task tumko karne hote hain jab tum AI se related task karte ho. To developers ko in tasks ko karne ke liye scratch se code likhna padhta hai, jo ek overhead hota hai.

To LangChain in tasks ko karne ke liye utilities provide karta hai.

LangChain ek framework hai jo AI se realted task ko perform karne ke liye utilities provide karta hai.

LangChain ek framework/library hai jo LLM-based applications banane ke liye use hoti hai. Ye do main programming languages mein available hai: **Python** aur **JavaScript/TypeScript**.

LangChain ek toolkit hai jo AI models ko:
- documents.
- memory.
- tools.
- databases.
- APIs.
- vector DBs.
- agents

ke saath connect karne mein help karta hai.

<br>

### Problem Kya Thi?

Suppose tum directly ek LLM use karna chahte ho.

Without LangChain tumhe manually:
- prompt banana padega.
- documents load karne padenge.
- embeddings generate karne padenge.
- vector DB connect karna padega.
- memory maintain karni padegi.
- API tools connect karne padenge.
- conversation history manage karni padegi.

Ye sab kaafi complex ho jata hai.

**Example Without LangChain**:

Suppose tum ek chatbot banana chahte ho jo:
- PDFs read kare.
- questions answer kare.
- memory maintain kare.

Without framework tumhe sab manually code karna padega.

Example:
```
pdf = load_pdf()
chunks = split_text(pdf)
embeddings = create_embeddings(chunks)
vector_db.store(embeddings)
query = user_input()
query_embedding = embed(query)
docs = similarity_search(query_embedding)
prompt = build_prompt(query, docs)
response = llm.generate(prompt)
```
Bahut saari cheeze manually manage karni padti hain

**LangChain Kya Karta Hai?**:

LangChain ye sab components ko ready-made building blocks ke form mein provide karta hai.

Yaani:
- loaders.
- chunkers.
- retrievers.
- memory.
- chains.
- agents.
- prompt templates.

already available hote hain.

Tum bas combine karo.

<br>

### LangChain Ka Main Purpose

LangChain mainly use hota hai:
- RAG applications.
- AI chatbots.
- AI agents.
- document Q&A systems.
- AI copilots.
- autonomous workflows.
- tool-using AI systems

banane ke liye.

<br>
<br>

### Installing LangChain for Python

command:
```
pip install -U langchain
pip install langchain-community
pip install pypdf
```

<br>
<br>

### LangChain ke main components

**1. Models**:

Models LangChain ka sabse foundational component hote hain. Model actual AI brain hota hai jo text ko understand karta hai aur response generate karta hai. Jab bhi user koi question puchta hai, ultimately model hi answer banata hai.
LangChain ka kaam model ko replace karna nahi hota, balki models ke saath interaction ko easy banana hota hai. Different AI providers ke APIs alag-alag hote hain. Kisi ka request format alag hota hai, kisi ka authentication alag hota hai, aur kisi ka response structure alag hota hai. LangChain ek common interface provide karta hai taaki developer easily multiple models ke saath kaam kar sake.

Agar future mein tum GPT se Claude ya kisi local model par shift karna chaho, toh application ka pura architecture rewrite nahi karna padega. LangChain abstraction layer provide karta hai.

Problem Without LangChain

Har provider ka API different hota hai.

Example:

OpenAI syntax:
```
client.chat.completions.create()
```

LangChain Kya Karta Hai?

Common interface provide karta hai.

Example:
```
from langchain.chat_models import ChatOpenAI

llm = ChatOpenAI()
```
Ab backend model change karna easy ho gaya.

<br>

**2. Prompt Templates**:

Prompt woh instruction hoti hai jo LLM ko di jati hai. AI ka output largely prompt quality par depend karta hai. Agar prompt clear aur structured ho toh answer bhi better aata hai.

LangChain prompt templates provide karta hai jisse prompts dynamic aur reusable ban jate hain. Hardcoded prompts maintain karna difficult hota hai, especially jab application large ho jaye.

Prompt templates mein placeholders hote hain jahan runtime par dynamic values inject hoti hain. Isse ek hi prompt structure multiple inputs ke liye reuse ho sakta hai.

Example
```
template = """
Explain {topic} in detail.
"""
```
User input:
```
Kubernetes
```
Final prompt:
```
Explain Kubernetes in detail.
```

<br>

**3. Chains**:

Chains LangChain ka core concept hain. “Chain” ka matlab hai multiple steps ko sequence mein connect karna. Ek step ka output next step ka input ban jata hai.

Real AI applications mein usually sirf ek LLM call nahi hoti. Multiple operations perform hote hain:
- input processing.
- retrieval.
- summarization.
- reasoning
- formatting.

LangChain in workflows ko modular chains ke form mein organize karta hai.

<br>

**4. Memory**:

LLMs naturally stateless hote hain. Unhe previous conversations automatically yaad nahi rehti. Agar memory system na ho toh har message isolated lagega.

LangChain memory components provide karta hai jo previous conversation history ko preserve karte hain aur future prompts mein inject karte hain.

<br>

**5. Document Loaders**:

Document loaders ka kaam external data sources se content load karna hota hai. RAG systems ka starting point usually document loading hi hota hai.

Different file formats aur platforms ke liye alag loaders hote hain. Loader text extract karta hai aur metadata bhi attach karta hai.

Example:
```
loader = PyPDFLoader("k8s.pdf")
```

<br>

**6. Text Splitters**:

Large documents ko directly LLM ko dena practical nahi hota kyunki:
- token limits hoti hain.
- cost increase hoti hai.
- irrelevant information aa sakti hai.

Isliye documents ko smaller chunks mein divide kiya jata hai. Text splitters ka kaam meaningful chunks create karna hota hai.

Example:
```
splitter = RecursiveCharacterTextSplitter(
    chunk_size=500,
    chunk_overlap=100
)
```

<br>

**7. Embeddings**:

Embeddings text ka mathematical representation hote hain. Ye semantic meaning ko vectors ke form mein represent karte hain.

Embedding Models:
- OpenAI embeddings
- BGE
- Sentence Transformers

Example:
```
embeddings = OpenAIEmbeddings()
```

<br>

**8. Vector Stores**:

Embeddings ko store karne aur similarity search perform karne ke liye vector stores use hote hain.

Traditional SQL databases exact matching ke liye optimized hote hain. Lekin vector databases semantic similarity search ke liye optimized hote hain.

Example:
```
db = Chroma.from_documents(
    chunks,
    embeddings
)
```

