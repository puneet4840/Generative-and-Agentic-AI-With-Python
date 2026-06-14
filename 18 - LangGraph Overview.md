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

LangGraph ek framework hai jo AI workflows ko graph structure mein represent karta hai.

Graph = Nodes + Connections.

Graph mein do cheeze hoti hain:

**1. Nodes**:

Nodes = Work karne wale components.

Example:
```
LLM Node
Search Node
Database Node
Tool Node
Human Approval Node
```

**2. Edges**:

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

