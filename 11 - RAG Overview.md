# RAG Overview

RAG ka full form hota hai: **Retrieval-Augmented Generation**.

RAG ek technique hai jisme LLM (Large Language Model) jaise OpenAI ke models aur external knowledge/data sources jaise PDF, Word documents ko combine kiya jata hai taaki AI data sources se accurate, updated, aur context-aware answers de sake.

Iska matlab hai ki hum LLM model ko text data dete hain jaise PDFs, Word Documents aur LLM model us data mein se user ka question dhoond ke nikalta hai. Isi ko RAG kehte hain.

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


