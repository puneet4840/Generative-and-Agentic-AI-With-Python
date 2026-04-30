# Advanced Promt Engineering Techniques

<br>

### Prompt Kya Hota Hai?

Prompt wo instruction, question, ya context hota hai jo tum AI ko dete ho taaki wo desired output generate kare.

<br>

### Prompt Engineering Kya Hai?

Prompt Engineering ka matlab hai AI (jaise ChatGPT, Claude, Gemini, etc.) ko is tarah instructions dena ki wo sabse accurate, useful, aur desired output de.

Iska matlab hai AI ko aise instructions dena jisse wo exactly wahi output de jo tum chahte ho.

<br>

### AI PROMPT KO ACTUALLY SAMJHTA KAISE HAI?

AI human ki tarah nahi sochta hai.

**AI kya karta hai?**:

AI patterns predict karta hai based on:
- Training data.
- Language probability.
- Context.
- Instructions priority.

Example:

**Weak Prompt**:
```
“Write a blog on Docker”
```
AI guess karega generic blog.

**Strong Prompt**:
```
“Act as a senior DevOps engineer and write a beginner-friendly detailed blog on Docker architecture, containers vs VMs, use cases, and commands.”
```
Ab AI ka direction clear hai. Ab AI ekdum thik prompt dega.

<br>
<br>

### PROMPT KE MAIN COMPONENTS

**1 - ROLE**:

AI ko kaun banna hai?

Example:
- “Act as a Kubernetes expert”.
- “Act as a Linux trainer”.
- “Act as a security auditor”.

Example:
```
Tum ek senior DevOps architect ho
```

Why?
- Role AI ke tone aur expertise ko shape karta hai.

<br>

**2 - TASK**:

Iska matlab hai ki AI se Karna kya hai?

Example:
- Explain
- Compare
- Write
- Summarize
- Troubleshoot

Example:
```
Mujhe CI/CD pipeline design karo
```

<br>

**3 - Context**:

Task ke baare mein background dena matlab task ki thodi detail dena.

Example:
- “User beginner hai”.
- “Production environment hai”.
- “Azure use ho raha hai”.

Example:
```
AWS aur Kubernetes environment ke liye.
```

<br>

**4 - CONSTRAINTS**

Rules define karo. Matlab kuch rules dena jiske according AI output generate kare.

Example:
- 500 words.
- Table format.
- Hinglish.
- Step-by-step.
- No jargon.

<br>

**5 - OUTPUT FORMAT**:

Output kaisa ho?

Example:
- Bullet points
- JSON
- YAML
- Markdown
- Table

Example:
```
Step-by-step notes with diagrams.
```

<br>

**Full Example**:
```
Tum ek senior Kubernetes trainer ho. Mujhe Kubernetes networking ko beginner se advanced Hinglish notes mein samjhao with examples, YAML, aur troubleshooting.
```

<br>
<br>

## Types of Prompting

Prompting multiple types ki hoti hai, Jaise:
- Zero-Shot Prompting.
- One-Shot Prompting.
- Few-Shot Prompting.
- Chain of Thought (CoT).
- Context Engineering.

<br>

### Zero-shot Prompting Technique

Zero-shot prompting ka concept simple hai: tum model ko bina koi example diye directly task perform karne ko bolte ho. Isme model apni pre-existing knowledge (training data) ka use karke result nikalta hai.

Zero-shot promting ka matlab hai ki tum LLM model ko bina kisi example ke direct task perform karne kehte ho.

Zero-shot un tasks ke liye best hai jo straightforward hain. Agar task complex hai aur tum zero-shot use kar rahe ho bina clear instructions ke, toh tum output ki quality se compromise kar rahe ho.

**Example-1:  Translation**:

Prompt:
```
"Is sentence ko Spanish mein translate karo: 'Main kal tumse milunga.'"
```
Response:
```
"Te veré mañana."
```

**Example-2: Summarization**:

Prompt:
```
"Is paragraph ki ek line mein summary likho: [Yahan koi bada news article paste karein]"
```
Response:
```
[AI us article ki main point ek line mein de dega.]
```

**Example-3: Creative Writing**:

Prompt:
```
"Ek naye coffee shop ke liye 3 catchy naam suggest karo jo dosti par based hon."
```
Response:
```
1. Chai-Chum, 2. The Friends' Brew, 3. Yaara Cafe.
```

**Example-4: Tone Shifting**:

Prompt:
```
"Is gusse wale message ko ek polite professional email mein badlo: 'Tumne kaam time pe nahi kiya, mujhe abhi report chahiye!'"
```
Response:
```
"Dear [Name], I noticed the report is pending. Could you please share it at your earliest convenience?"
```

<br>

**Zero-shot kab use karein?**:
- Jab aapka kaam bahut common ho (jaise translation ya summary banana).
- Jab aapke paas AI ko dikhane ke liye koi examples na hon.
- Jab aap jaldi mein ho aur bas ek seedha sawal puchna chahte hon.

<br>

**Good Zero-Shot Prompt Design**:

Rule 1: Clear Instruction:

Bad Prompt:
```
“Tell me about security.”
```
Good Prompt:
```
“Explain cloud security best practices for AWS beginners.”
```

Rule 2: Role Assignment

Example:
```
“You are a senior DevOps architect. Explain CI/CD.”
```

Rule 3: Output Formatting

Example:
```
“List top 10 Linux commands in table format.”
```


<br>

### Python Example with Zero-Shot Prompting

Python Code ```zero-shot-prompting.py:
```
# Zero-Shot Prompting 

from openai import OpenAI
client = OpenAI(
    api_key="AIzaSyCyQrDCJaT3OV_62gwb46DOGZFN9P3O9q0",
    base_url="https://generativelanguage.googleapis.com/v1beta/openai/"

)

response = client.chat.completions.create(
    model="gemini-3-flash-preview", 
    messages=[
        {"role": "user", "content": "Hi, how are you? Isko french mein translate kar do?"}
    ]
)

print(response.choices[0].message.content)
```

Response:
```
"Hi, how are you?" ko French mein translate karne ke kuch tarike hain, jo situation par depend karte hain:

1. **Informal (Doston ya barabar walo ke liye):**
   * **Salut, ça va ?** (सा-लू, सा-वा?)
   * **Salut, comment vas-tu ?** (सा-लू, को-मों वा-तू?)

2. **Formal (Bado ke liye, office mein, ya anjaan logo ke liye):**
   * **Bonjour, comment allez-vous ?** (बों-झूर, को-मों ता-ले-वू?)

**Short summary:**
* Hi = **Salut** (informal) / **Bonjour** (formal)
* How are you? = **Ça va ?** or **Comment allez-vous ?**
```

<br>
<br>

### One-Shot Prompting Technique

One-shot prompting ka matlab hai: AI ko task samjhane ke liye sirf EK example dena, aur phir usse same pattern follow karne ko kehna.

Matlab One-shot technique mein instruction ke saath ek example deke samjhate hain ki ye karna hai.

Yaani:
- 1 instruction.
- 1 sample example.
- Then actual task.

One-shot prompting ka matlab hai AI ko koi task karne ke liye kehna aur uske saath sirf ek example dena.

Jab zero-shot prompting (bina example ke) se AI aapka matalab puri tarah nahi samajh pata, tab one-shot prompting kaam aati hai. Is ek example se AI ko yeh samajh aa jata hai ki aapko output kis format, style ya tone mein chahiye.

**Example**:

Prompt:
```
Convert informal message into professional email.

Informal: I can't come tomorrow because I am sick.
Professional: I am unable to attend tomorrow due to illness.

Informal: I need more time to finish this project.
Professional:
```
Response:
```
I would like to request additional time to complete this project.
```

**Example-2: Text Classification**:

Prompt:
```
Classify sentiment as Positive or Negative.

Text: This laptop is amazing and super fast.
Sentiment: Positive

Text: This phone battery dies too quickly.
Sentiment:
```
Response:
```
Negative
```

**Example-3: Translation**:

Prompt:
```
Translate English to Hindi.

English: Good morning
Hindi: सुप्रभात

English: How are you?
Hindi:
```
Response:
```
आप कैसे हैं?
```

**Example-4: Coding**:

Prompt:
```
Convert requirement into Python function.

Requirement: Add two numbers
Code:
def add(a, b):
    return a + b

Requirement: Multiply two numbers
Code:
```
Response:
```
def multiply(a, b):
    return a * b
```

<br>
<br>

### Few-Shot Prompting

Few-shot prompting ka matlab hai: AI ko task samjhane ke liye multiple examples dena (usually 2–5 ya usse zyada), taaki woh pattern ko aur clearly samjhe.

Yaani:
- Instruction
- Multiple examples
- New task

Jab Zero-shot (no example) aur One-shot (1 example) se AI ko confuse hota hai ya woh aapka pattern nahi pakad paata, tab Few-shot sabse best kaam karta hai. Isse AI ko "pattern" aur "nuances" (bareekiyan) samajh aa jati hain.

**Real Life Example**:

Maan lijiye aap AI se Hinglish sentences ko "English-Professional" mein convert karwana chahte hain:
```
Example 1: "Yaar, meeting cancel ho gayi kya?" -> "Has the meeting been cancelled?"

Example 2: "Mujhe report kal tak chahiye hi chahiye." -> "I require the report by tomorrow, without fail."

Example 3: "Aaj thoda late ho jayega aane mein." -> "I will be arriving a bit late today."

Task (Aapka Sawaal): "Tumne abhi tak mail ka reply kyun nahi diya?" ->
AI ka Output: "Why haven't you replied to the email yet?"

Yahan 3 examples dekh kar AI samajh gaya ki use "Yaar" jaise words hatane hain aur tone ko Professional rakhna hai.
```

**Practical Example**:

Maano tumhe ek automation script ke liye logs ko categorize karna hai. Direct bolne par AI confuse ho sakta hai, isliye tum use training dete ho:

Task: Niche diye gaye technical logs ko "Category" aur "Priority" mein divide karo.

Prompt:
```
Example 1:
Log: "Disk space at 95% on Server-01"
Output: [Category: Infrastructure] [Priority: High]

Example 2:
Log: "New user 'puneet_dev' created"
Output: [Category: IAM] [Priority: Low]

Example 3:
Log: "Kubernetes Pod 'nginx-404' restarted unexpectedly"
Output: [Category: Orchestration] [Priority: Critical]

Actual Task (Ab tum karo):
Log: "Terraform apply failed: Provider credential expired"
```
Response:
```
AI Output: [Category: Automation/Cloud] [Priority: High]
```

**Example**:

Prompt:
```
Classify as Spam or Not Spam.

Message: Win a free iPhone now!
Label: Spam

Message: Your bank OTP is 1234
Label: Not Spam

Message: Claim your reward today
Label: Spam

Message: Meeting at 5 PM
Label:
```
Response:
```
Not Spam
```

**Example**:

Prompt:
```
Convert casual to professional.

Casual: Send me this ASAP
Professional: Could you please send this at the earliest convenience?

Casual: Fix this now
Professional: Could you please address this issue promptly?

Casual: Call me now
Professional:
```
Response:
```
Could you please call me at your earliest convenience?
```

### Python Example with Few-Shot Prompting

```zero-shot_prompting.py```:
```
# Few-Shot Prompting

from openai import OpenAI
client = OpenAI(
    api_key="AIzaSyCyQrDCJaT3OV_62gwb46DOGZFN9P3O9q0",
    base_url="https://generativelanguage.googleapis.com/v1beta/openai/"

)

Sytem_Prompt = """
Do not answer anything except coding related questions otherwise just say sorry"

Exampple-1: 
Tell me a joke.
Answer: Sorry, I can only answer coding related questions.

Example-2:
What is a + b whole square?
Answer: Sorry, I can only answer coding related questions.
"""

response = client.chat.completions.create(
    model="gemini-3-flash-preview", 
    messages=[
        {"role": "system", "content": Sytem_Prompt},
        {"role": "user", "content": "Write a Python function to calculate the area of a circle."}
    ]
)

print(response.choices[0].message.content)
```

Response:
```
import math

def calculate_circle_area(radius):
    return math.pi * (radius ** 2)
```

