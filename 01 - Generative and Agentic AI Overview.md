# Overview of Generative and Agentic AI

<br>
<br>

## Generative AI Architecture Hierarchy

### 1. Foundation Models (The Core)

Ye base hai jahan se sab shuru hota hai:

**1 - LLMs (Large Language Models)**: Text generate karne ke liye (GPT-4, Claude, Llama 3).

**2 - Diffusion Models**: Images generate karne ke liye (Midjourney, Stable Diffusion).

<br>

### 2. Implementation Layer (Yahan se tumhari padhai shuru hogi)

Agar tumhe directly coding/implementation karni hai, toh ye 3 pillars hain:

**1 - RAG (Retrieval-Augmented Generation)**: * Kyun? Kyunki LLM ko duniya ki har cheez nahi pata hoti (jaise tumhari company ka private data). RAG ke zariye hum LLM ko external documents "padhne" ko dete hain.

  - Kya seekhna hai? Vector Databases (Pinecone, ChromaDB), Embeddings, aur Document Loaders.

**2 - Fine-Tuning (PEFT/LoRA)**: * Kyun? Jab tumhe model ka "lehja" badalna ho ya use kisi specific domain (medical/legal) ki gehrai sikhani ho.

  - Kya seekhna hai? Dataset preparation aur HuggingFace library.

<br>

### 3. Orchestration Frameworks (The Glue):

- Kyun? LLM ko aur tools (Python, Google Search, SQL) se jodne ke liye.

- Kya seekhna hai? LangChain ya LlamaIndex. Ye sabse important hain.

<br>
<br>

## Building Towards Agentic AI

Tumne "Agentic AI" ka zikr kiya tha. Ye GenAI ki sabse advanced stage hai. Iska workflow aise chalta hai:

- Reasoning: LLM ko ek task diya gaya (e.g., "Mera flight ticket book karo").
- Planning: AI khud steps banata hai.
- Tool Use: AI khud API call karta hai ya internet search karta hai.
- Reflection: AI check karta hai ki kya usne sahi kiya? Agar nahi, toh wapas try karta hai.

<br>
<br>
<br>
<br>

### Generative AI Kya Hoti Hai?

