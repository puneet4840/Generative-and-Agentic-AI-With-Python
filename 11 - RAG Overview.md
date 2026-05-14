# RAG Overview

RAG ka full form hota hai: **Retrieval-Augmented Generation**.

RAG ek technique hai jisme LLM (Large Language Model) jaise OpenAI ke models aur external knowledge/data sources jaise PDF, Word documents ko combine kiya jata hai taaki AI data sources se accurate, updated, aur context-aware answers de sake.

Iska matlab hai ki hum LLM model ko text data dete hain jaise PDFs, Word Documents aur LLM model us data mein se user ka question dhoond ke nikalta hai. Isi ko RAG kehte hain.

<br>

2020–2022 ke beech jab GPT-3 aaya, log bahut excited hue. Lekin ek baat clear ho gayi jaldi hi — yeh model bahut intelligent tha, lekin "closed box" tha. Isko sirf wahi pata tha jo training data mein tha. Company-specific documents? Nahi pata. Last week ki news? Nahi pata. Tumhari organization ki internal policies? Bilkul nahi pata.

Phir ek aur problem thi — jab model ko nahi pata hota tha, toh woh chup nahi rehta tha. Woh confidently galat cheezein bol deta tha. Isko "hallucination" kehte hain. Ek doctor ne medical chatbot se pucha, usne ek aisi dawai suggest ki jo exist hi nahi karti — lekin itne confidence ke saath boli ke doctor ko doubt hi nahi hua. Yeh dangerous tha.

Toh researchers ne socha — kya koi aisa tarika hai jisse LLM ko runtime par relevant information diya jaaye? Jaise ek student ko exam ke time open book de do?
Yahi se RAG ka idea aaya. 2020 mein Facebook AI Research (FAIR) ne ek paper publish kiya — "Retrieval-Augmented Generation for Knowledge-Intensive NLP Tasks" — aur AI ki duniya badal gayi.

<br>
<br>

### Problem Kya Thi Without RAG?

Normal LLM kaise kaam karta hai?

LLM:
- internet ke huge data par train hota hai.
- patterns learn karta hai.
- phir next words predict karta hai

Example:

Agar tum pucho:
```
“Kubernetes mein kube-proxy ka role kya hai?”
```

LLM apni training memory se answer de dega.

Lekin issue:

**Problem 1: Knowledge Old Ho Sakta Hai**:

Model ki training kisi date tak hoti hai.

Example:
- Model 2024 tak train hua. Tum 2026 ka AWS feature puch rahe ho.

Model ko pata hi nahi hoga.

<br>

**Problem 2: Hallucination**:

Kabhi-kabhi LLM confident fake answers deta hai.

Example:

Tum pucho:
```
“Hamari company ka leave policy kya hai?”
```
LLM:
- company ko janta hi nahi.
- fir bhi answer bana dega.

Ye dangerous hai.

<br>

**Problem 3: Private Data Access Nahi**

LLM ko:
- company PDFs
- Confluence docs
- Jira tickets
- Slack chats
- internal database

ka access nahi hota.

Toh organization-specific answers possible nahi hote.

To RAG is problem ko solve karta hai.

<br>

**RAG Is Problem Ko Kaise Solve Karta Hai?**:

RAG mein hum AI ko bolte hain: “Pehle relevant information data mein search karo, phir us basis par answer generate karo.”

Yaani:
```
Question → Search Relevant Data → Pass to LLM → Generate Answer
```
Isi ko Retrieval-Augmented Generation kehte hain.

Matlab hum LLM model ko alag se data dete hain aur model us data mein user ki query search karta hai aur answer deta hai.

<br>
<br>

### Real-Life Analogy

Suppose tum ek exam dene ja rahe ho.

**Without RAG**:

Tum sirf memory se answer de rahe ho.
- yaad galat ho sakti hai
- outdated ho sakta hai

**With RAG**:

Tum:
- pehle book kholo
- relevant chapter dhoondo
- fir answer likho

Exactly yehi RAG karta hai.

<br>
<br>

### RAG kaam kaise karta hai?

RAG ka working process 2 parts mein divided hota hai:
- Indexing Phase.
- Query Phase.

<br>

### Indexing Phase

Indexing phase mein data ko chunks mein divide kiya jata hai aur vector db mein store kiya jata hai.

Indexing phase mein bhi multiple phases hote hain.

**Step-1: Data Collection**:

RAG system data collect karta hai.

Sabse pehle RAG system ko knowledge chahiye hoti hai. Ye knowledge kahin se bhi aa sakti hai, Jaise:
- PDFs
- DOCX files
- company wiki
- Confluence
- SharePoint
- GitHub repositories
- Kubernetes YAML files
- Terraform modules
- Slack chats
- databases
- websites

System ke paas loaders hote hain. Different file types ke liye different parsers hote hain.

Example:
- PDF parser
- HTML parser
- Markdown parser
- GitHub loader

Ye loaders actual text extract karte hain.

Suppose PDF mein likha hai:
```
If pod enters CrashLoopBackOff:
1. Check logs
2. Verify probes
3. Inspect events
```
System is text ko extract kar lega.

**Metadata Collection**:

Sirf text hi important nahi hota.

Metadata bhi important hota hai.

Metadata means:
extra information about document.

Example:
```
{
  "source": "runbook.pdf",
  "page": 12,
  "team": "devops",
  "environment": "production"
}
```
Ye metadata later filtering mein bahut useful hota hai. Suppose user specifically production docs search karna chahta hai. Tab metadata help karega.

<br>

**Step 2 — Document Cleaning**:

Raw data usually messy hota hai. Agar directly embeddings bana diye toh retrieval quality kharab ho sakti hai. Isliye data ki cleaning hoti hai.

System:
- extra spaces remove karta hai.
- headers/footers remove karta hai.
- duplicate lines remove karta hai.
- HTML tags clean karta hai.
- garbage OCR text remove karta hai.

Example:

Before cleaning:
```
Page 1 of 42
CONFIDENTIAL

CrashLoopBackOff troubleshooting
```
After cleaning:
```
CrashLoopBackOff troubleshooting
```
Ye step quality improve karta hai.

<br>

**Step 3 — Chunking**:

Ab aata hai RAG ka bahut important concept: Chunking.

LLMs huge documents ko directly efficiently process nahi karte.

Agar tum pura 500-page PDF directly inject kar do:
- token limit exceed ho jayegi
- irrelevant context aa jayega
- cost badhegi
- performance degrade hogi

Isliye documents ko small-small logical pieces mein todte hain.

In pieces ko: chunks kehte hain.

Example-1:

Suppose ek 500 page ka pdf hai, Usko chunks mein break karna hai to ese kar sakte hain.
```
page 1 - 3 : Chunk-1
page 4 - 6 : Chunk-2
page 7 - 10: Chunk-3
```

Example-2:

Suppose ek pdf ka page hai, usko chunks mein break karna hai to paragraph by paragraph chunks mein break kar sakte hain.

Example-3:

Suppose ek Kubernetes guide hai.

Usme sections hain:
- deployments
- services
- ingress
- DNS
- storage

Agar pura document ek hi chunk hua: retrieval accurate nahi hoga.

Isliye system split karta hai.

Example:
```
Chunk 1 → Deployment basics
Chunk 2 → ReplicaSets
Chunk 3 → Rolling updates
Chunk 4 → Rollbacks
```
Ab retrieval precise ho sakta hai. Ese bhi chunks mein break kiya jata hai.

<br>

Chunk Size Important Kyun Hai?

Agar chunk bahut chhota hua context break ho jayega.

Example:
```
Line 1: Kubernetes deployments
Line 2: allow rolling updates
```
Agar split galat hua:
```
meaning destroy ho sakta hai.
```
Agar chunk bahut bada hua:
```
irrelevant information aa jayegi.
```

Typical Chunk Sizes Generally: 200–1000 tokens used hote hain. Isliye smart chunking bahut important engineering problem hai.

<br>

Overlapping Chunks:

Real-world RAG systems overlap use karte hain.

Example:
```
Chunk A → lines 1-100
Chunk B → lines 80-180
```

Overlap ka benefit:
- context continuity maintain rehti hai.

Suppose sentence line 95 se start hua aur line 110 tak gaya.

Without overlap sentence cut ho jayega. Overlap is issue ko solve karta hai.

<br>

**Step 4 — Embeddings**:

Is step mein text ko vectors mein convert kiya jata hai, vector ka matlab numbers ki list.

Embedding: text ka numerical vector representation hota hai.

Simple words mein: AI text ka meaning numbers mein convert karta hai.

Suppose sentence hai:
```
How to restart Kubernetes pod?
```
Embedding model ise convert karega:
```
[0.245, -0.992, 0.771, ...]
```
Ye vector hundreds ya thousands dimensions ka ho sakta hai.

Embedding words ko represent nahi karta. Meaning ko represent karta hai.

<br>

Embedding Model Internally Kya Karta Hai?

Embedding models generally transformer architecture use karte hain.

Ye:
- sentence context samajhte hain.
- word relationships analyze karte hain.
- semantic meaning encode karte hain.

Popular embedding systems:
- OpenAI embeddings
- BGE
- E5
- Sentence Transformers

<br>

**Step 5 — Vector Database Storage**:

Ab embeddings ko vector database mein store karna hota hai.

Traditional SQL DB yaha sufficient nahi hota. Kyuki yaha exact matching nahi karni. Semantic similarity search karni hoti hai.

Isliye Vector Database use hota hai.

Popular vector DBs:
- Pinecone
- Weaviate
- Qdrant
- Milvus

Vector DB Ka Core Kaam

Ye:
- embeddings store karta hai.
- similarity search optimize karta hai.
- nearest vectors quickly retrieve karta hai

Suppose millions embeddings stored hain. Har query par sab compare karna expensive hota.

Isliye optimized indexing algorithms use hote hain:
- HNSW
- IVF
- PQ

Ye ANN:
- Approximate Nearest Neighbor search enable karte hain.

<br>
<br>

### Query Phase

Ye RAG ka second phase hota hai. Is phase mein user ki query ko same vector model ka use karke vector embedding mein convert kiya jata hai, Fir vector database mein user ki query ke vector embedding jaise same semantic match wale vector find kiye jaate hain. Fir user ki normal query aur find kiye hue vector LLM model ko diye jaate hain. Fir LLM model response generate karta hai.


Yaha actual user interaction hota hai.

**Step 6 — User Question**:

Is step mein user apni query puchta hai, jo bhi user ko LLM se puchna ho.

User puchta hai:
```
Why is my pod restarting continuously?
```

<br>

**Step 7 — Query Embedding**:

Jaise uper ke steps mein documents embeddings mein convert hue the, waise hi query bhi embedding mein convert hoti hai.

Question:
```
Why is my pod restarting continuously?
```
↓

Vector:
```
[0.661, -0.113, 0.991]
```

Documents aur queries same embedding model se vectorize hone chahiye. Otherwise vector space mismatch ho jayega.

<br>

**Step 8 — Similarity Search**:

Is step mein user ki query ke jo vector banaye the unko vector db documents ke similar vector chunks se compare karta hai matlab user ki query jaise chunks db mein find karta hai.

Query embedding generate hone ke baad vector database similarity search perform karta hai jahan query vector ko stored document vectors ke against compare kiya jata hai using techniques like cosine similarity. Agar vectors semantic space mein ek doosre ke close hote hain toh system un chunks ko relevant maanta hai aur retrieve karta hai. Isi mechanism ki wajah se user “pod restarting issue” likhe tab bhi system “CrashLoopBackOff troubleshooting” retrieve kar sakta hai.

Ab vector DB: user ke query vector ko stored document vectors ke saath compare karta hai.

Goal: most semantically relevant chunks find karna.

Example

User query:
```
pod restarting issue
```
Retrieved chunks ho sakte hain:
```
CrashLoopBackOff troubleshooting
Liveness probe failures
OOMKilled analysis
```
Even though exact words same nahi the, semantic meaning match ho gaya. Yehi embeddings ka power hai.

<br>

**Step 9 — Retrieval**:

Generally top-k chunks retrieve hote hain.

Example:
- top 3
- top 5
- top 10

chunks.

Ye chunks user query ke most relevant pieces hote hain.

<br>

**Step-10 - Re-ranking**:

Is step mein fir se perfect chunks ko find out kiya jata hai.

Initial vector retrieval fast hota hai lekin perfectly accurate nahi hota, isliye advanced RAG systems reranking stage use karte hain jahan retrieved chunks ko deeper contextual models evaluate karte hain. Rerankers query aur document relationships ko more detailed level par analyze karte hain aur best possible chunks ko final context ke liye select karte hain. Ye stage overall answer relevance aur grounding significantly improve karti hai.

<br>

**Step 11 — Context Assembly**:

Jab relevant chunks vector db se retrieve ho jate hain, tab:
- original user query.
- retrieved chunks/context.

dono ko combine karke LLM ko diya jata hai.

Is step mein user ki original query aur vector db se document se find kiye hue chunks dono ko combine karke LLM model ko diye jaate hain.

Yaani LLM ko sirf chunks nahi diye jate. Original question bhi diya jata hai, warna LLM ko samajh hi nahi aayega ki user kya puch raha hai.

Example:

Suppose user query hai:
```
How to debug CrashLoopBackOff in Kubernetes?
```

Step 1 — Query Embedding

Is query ka embedding bana:
```
[0.11, 0.77, -0.92]
```

Step 2 — Similarity Search

Vector DB ne top chunks retrieve kiye:
```
Chunk 1:
Use kubectl logs to inspect container crash.

Chunk 2:
Check liveness and readiness probes.

Chunk 3:
Use kubectl describe pod for events.
```

Step 3 — Final Prompt Construction

Ab actual LLM prompt kuch aisa banega:
```
You are a Kubernetes assistant.

Use ONLY the provided context.

Context:
---------
Use kubectl logs to inspect container crash.

Check liveness and readiness probes.

Use kubectl describe pod for events.

Question:
How to debug CrashLoopBackOff in Kubernetes?
```

Notice karo:
- Original user query abhi bhi present hai.
- Retrieved chunks bhi present hain

Dono combine hue.

<br>

**Step 12 — LLM Processing**:

Ab LLM ka actual generation phase start hota hai.

LLM:
- retrieved context read karta hai.
- relationships understand karta hai.
- reasoning perform karta hai.
- answer generate karta hai

Internally transformer attention mechanism use hota hai.

LLM har token ke relationships analyze karta hai.

Example

Context mein:
```
Check kubectl logs
Verify probes
```
LLM answer generate karega:
```
Your pod may be restarting because:
- application crash
- failed probes
- OOMKilled issue
```

<br>

**Step 14 — Final Response**:

Ab user ko final grounded response milta hai.

Ye response:
```
retrieved docs based hota hai
updated ho sakta hai
organization-specific ho sakta hai
```
Isi wajah se RAG enterprise AI ka foundation ban gaya hai.

<br>

**Final End-to-End Flow**:

Pure system ko ek baar fir visualize karo:
```
Documents
   ↓
Cleaning
   ↓
Chunking
   ↓
Embeddings
   ↓
Vector Database
   ↓
User Question
   ↓
Query Embedding
   ↓
Similarity Search
   ↓
Top Relevant Chunks
   ↓
Prompt Injection
   ↓
LLM Generation
   ↓
Final Accurate Response
```
