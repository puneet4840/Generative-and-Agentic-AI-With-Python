# Lang Graph Overview

LangGraph ek framework hai, jo langchain ke makers ne banaya hai, jo AI Agents banane ke liye use hota hai.

Agar tumne LangChain ke baare mein suna hai, to LangGraph ko LangChain ka advanced version samajh sakte ho jo stateful, multi-step aur autonomous AI agents banane ke liye design kiya gaya hai.

Simple words mein:
- LangChain = Linear Workflow.
- LangGraph = Graph-Based Workflow.

<br>

### Problem Kya Thi?

Pehle jab AI applications banti thi, workflow kuch aisa hota tha:
```
User Query
     ↓
LLM
     ↓
Tool Call
     ↓
LLM
     ↓
Response
```
Ye ek linear workflow hai.

Lekin maan lo tum ek DevOps AI Assistant bana rahe ho jo:
- Kubernetes logs analyze kare.
- AWS resources check kare.
- Terraform code validate kare.
- Error aaye to dubara try kare.
- Human approval le.
- Multiple tools use kare.

To workflow linear nahi rahega. AI ko baar-baar decisions lene padenge.

Example:
```
User: EC2 down hai

AI:
  ↓
CloudWatch check karo
  ↓
Error mila?
  ↓
Yes
  ↓
EC2 status check karo
  ↓
Still issue?
  ↓
Logs check karo
  ↓
Root cause identify karo
  ↓
User ko batao
```
Yahan AI ek graph mein move kar raha hai. Jahan multiple decision lene pad rhe hain. Isi problem ko solve karne ke liye LangGraph bana.

<br>

### Componenets of Lang graph.

LangGraph ek framework hai jo AI workflows ko graph structure mein represent karta hai.

Graph = Nodes + Connections.

LangGraph mein 3 components hote hain:
- Nodes.
- Edges.
- State.

<br>

**1. Nodes**:

Nodes function hote hain, jo kuch action perform karte hain. Jaise, ek function user input lena, dusra function kisi tool ko call karna.

Nodes = Work karne wale components.

Tumko in nodes ko edges ke through apas mein connect karna hote hai.

Example:
```
LLM Node
Search Node
Database Node
Tool Node
Human Approval Node
```

<br>

**2. Edges**:

Edges are the connection between the nodes.

Edges decide karte hain ki next node kaun sa execute hoga.

Example:
```
Node A → Node B
Node B → Node C
```

ya

```
Node B
   ↓
Error?
 ↓      ↓
Yes     No
 ↓       ↓
Retry   Finish
```

<br>

**3. State**:

State ek piece of data hota hai jo hum graph ko as an input dete hain.

State ek shared memory hoti hai jo sabhi Nodes ke beech pass hoti hai. Har node isme se purani info padh sakta hai aur apni nayi info add kar sakta hai.

Jab aapka AI workflow chal raha hota hai, toh ek node se dusre node par jo bhi data ya information pass hoti hai, use hum State kehte hain. Graph ke andar jitne bhi Nodes (Python functions ya AI agents) hote hain, woh sab isi ek common State ko padhte (read) aur badalte (update) hain.

Example:

Maan lijiye user ne pucha: "Weather in Delhi".

Start: State khali hai, bas user_query: "Weather in Delhi" save hai.
```
state{
user_query: Weather in Delhi.
}
```

Node 1 (Search Agent): Yeh State se query padhta hai. Web search karke data lata hai aur State ko update kar deta hai:
```
state{
user_query: [Weather in Delhi],
search_results: ["Delhi weather is 32°C and sunny"]
}
```

Node 2 (Writer Agent): Yeh State mein se search_results ko uthata hai, ek accha sa reply banta hai, aur State mein jod deta hai:
```
state{
user_query: [Weather in Delhi],
search_results: ["Delhi weather is 32°C and sunny"],
final_answer: ["Hello! Delhi mein aaj dhoop hai aur temperature 32°C hai.]
}
```

End: User ko final_answer dikha diya jata hai.


<br>
<br>

### Real Life Example 1

Tum ek DevOps AI Assistant bana rahe ho.

User:
```
My pod is crashing.
```

Normal LLM:
```
Possible reasons:
OOM
CrashLoopBackOff
Config issue
```
Generic answer dega.

LangGraph Agent:
```
User Query
      ↓

Check Pod Status
      ↓

Check Logs
      ↓

Analyze Error
      ↓

Find Root Cause
      ↓

Suggest Fix
```

Output:
```
Root Cause:
Container killed due to memory exhaustion.

Fix:
Increase memory limit from 256Mi to 512Mi.
```

<br>

### Real Life Example 2

AWS Troubleshooting Agent

User:
```
EC2 instance unreachable.
```

LangGraph:
```
Start
  ↓

Check EC2 Status

  ↓

Running?

 ↓      ↓

No      Yes

 ↓        ↓

Start   Check Security Group

             ↓

        Check NACL

             ↓

        Check Route Table

             ↓

          Solution
```

Notice:
- AI har step pe decision le raha hai.
- Isi wajah se iska naam Graph hai.

<br>
<br>
<br>

## Installing the LangGraph

Command:
```
pip install -U langgraph
```
