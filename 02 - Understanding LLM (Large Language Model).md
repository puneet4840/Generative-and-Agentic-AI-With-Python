# Understaning LL (Large Language Model)

### LLM (Large Language Model) kya hai?

LLM (Large Language Model) ek AI model hai jo human language matlab text ko samjta hai aur generate karta hai. 

Matlab human ek text input LLM ko deta hai aur LLM us text ko process karke uska output text form mein deta hai. Matlab LLM text generate karta hai.

Ye deep learning ke saath neural networks ka use karke text ko generate karta hai jo human ki tarah feel hota hai.

- **Large**: Isse bohot bade data (internet, books, articles) par train kiya jata hai.
- **Language**: Yeh human language (Hindi, English, etc.) ko samajhta hai.
- **Model**: Yeh ek AI neural network hai jo predict karta hai ki sentence mein agla shabd kya hona chahiye.

Generate AI 4 types ke hote hain, usme se ek type hota hai transformer, LLM models transformer technique ka use karte hain.

Example:
- Tum likho: "Mujhe ek email likh do boss ko leave ke liye"
- LLM turant ek proper professional email bana dega.

<br>

**Basic Idea**:

LLM ka kaam hai:
- Next word predict karna based on previous words.

LLMs agle word ko predict karte hain poore sentence ko analyse karke.

Example:
```
"India is a ______ country"
```
LLM guess karega:
- "developing"
- "diverse"
- "beautiful"

Ye guess random nahi hota — ye **probability + training data** pe based hota hai.

<br>
<br>

### History of LLM

Actual kahani shuru hoti hai 2017 se, jab google ke 8 scientists ne ek research paper nikala jiska naam tha ```Attention Is All You Need```.

Is paper ka focus tha **Attention Mechanism** par.

Ye paper kehta tha ki ```Ek word, sentence ke ander other words par relate kare```.

Iska matlab hai ki LLM jab bhi koi word generate kare to vo sentence ke ander jo word LLM ne pehle generate kar diye hain un words se relate kare. Esa nhi ho na chiaye ki LLM jo word generate karne wala hai vo poore sentence mein kisi word se relate na kar.

Example:
```
Ram is a boy. He is a good in study.
```

Ye ```He``` word ```Ram``` se relate kar rha hai.


Example:
```
"The server crashed because it was overloaded"
```

Yahan ``` it``` word ```server``` se relate kar rha hai.

<br>

**Problem kya thi Transformer Model se pehle**:

Transformer Model aane se pehle Neural Networks ke kuch models use hote the, Jaise Recurrent Neural Networks (RNN), Long Short-Term Memory (LSTM) and Gated Recurrent Unit (GRU).

To Recurrent Neural Networks (RNN), sequential data matlab text format wale data ko process kar sakta the aur thoda context yaad rakhta tha. Yeh model sentence ko word-by-word process karke previous words ka influence next prediction mein use karte tha. Lekin inmein long-term memory weak thi, isliye lambi sentences mein context lose ho jaata tha.

RNN ki limitations ko solve karne ke liye LSTM aur GRU jaise models aaye, jo important information ko selectively store aur forget kar sakte the. Yeh models better context handling provide karte the, especially longer sentences ke liye. Fir bhi yeh sequential processing pe dependent the, jisse training slow hoti thi aur scalability limited thi.

LLM se pehle ke systems ya to rules follow karte the, ya probabilities calculate karte the, ya limited memory neural networks use karte the. In sab approaches mein ek common limitation thi — yeh language ka deep contextual meaning properly understand nahi kar paate the. Isi limitation ko solve karne ke liye baad mein transformer-based LLMs aaye, jo aaj ke modern AI ka base hain.

<br>

**Google ne paper mein kya kaha?**

Paper ka main statement:
- Sequence ko samajhne ke liye recurrence (RNN) ya convolution (CNN) ki zarurat hi nahi hai.

Instead:
- Sirf “Attention Mechanism” se hi kaam ho sakta hai.

Isliye naam:
- “Attention Is All You Need” rakah gya.

<br>

**Attention ka Basic Concept**:

Socho tum ek sentence padh rahe ho: “The animal didn’t cross the street because **it** was too tired.”

Question: “it” kis ke liye use hua hai?

Tumhara brain automatically:
- “animal” pe focus karega.
- “street” ignore karega.

Ye hi hai Attention.

Model bhi same karta hai — important words pe focus karta hai.

<br>
<br>

### Transformer Model kaam kaise karta hai?

Jo bhi tum input transformer model ko dete ho, us input ko token mein break kiya jata hai.

Token ka matlab hai ek sentence ko chote chote parts mein break karna.

To token ka matlab hai jaise ek sentence "I love ChatGPT", Isko small parts mein break karna:
```
[I] [Love] [Chat] [GPT]
```
Isi ko tokenization bolte hain. Words mein break karna.


Example:

Sentence:
- “Hey There”


Transformer pehle input sentence ko token mein break karega, words ko number assign karega.
```
[Hey]=10
[There]=20
```

Fir **Autoregressive Language Modeling** technique se next word predict karta hai. 

Ab jo bhi output prediction mein aata hai usko complete sentence mein add karke as a input use karta hai aur next word predict karta hai.

Ye process har baar repeat hoti hai aur text generate hota jata hai.

Vaise iske peeche kaami process hoti hai, humne yaha pe ye short mein samjhi hai, aage hum ise detail mein dekhenge.

<br>

<img src="https://drive.google.com/uc?export=view&id=1hsoMRXtFMPcRfmAL6hutb2oMWlqbQHPo" width="620" height="340">

<br>

Explanation:
- Suppose aapne kisi bhi LLM model ko ```Hey There``` likha as a input/
- Ab LLM model is sentence ko tokens mein divide karega, token ka matlab hai sentence ko ek ek single word mein break karega.
- Fir har token as a input lega.
- Ab ```Autoregressive Language Modeling``` technique se next word ko predict karega. Jaise output aaya ```I```.
- Ab is output ko input sentence mein add karega jaise ```Hey There I```. Ab is complete sentence ko as a input dekhega.
- Fir inko tokens mein break karega aur ```Autoregressive Language Modeling``` karke next word predict karega. Jaie ab output aaya ```am```.
- Fir is output ```Hey There I am``` ko next iteration mein as a input lega, token mein break karega aur next word predict karega.

Ese ye transformer model kaam karta hai, aur saare LLMs bhi isi model pe based hote hain isi tarah kaam karete hain.

User ko direct token ke form mein output nahi dikhta hai, User ko token de-tokenize karke matlab fir token se word ya character mein tranform karke output dikhaya jata hai.

<br>
<br>

### LLM Kaise Work Karta Hai?

**LLM Kya hota hai**>

LLM (Large Language Model) ka main kaam hai: “given context ke basis pe next word predict karna”.

LLM ka kaam kai next word predict karna.

Example:
```
Input: "I love to drink"
```
Model guess karega: ```"tea"```, ```"coffee"```, ```"water"```.

Lekin yeh sirf surface level baat hai.

<br>

**Real mein kya hota hai?**

Jab tum likhte ho:
```
I love to drink
```
Model ke dimaag mein yeh hota hai:
- Yeh sentence incomplete hai.
- Next word kya koi liquid hoga.
- Grammar ke hisaab se noun aayega.
- Context ke hisaab se "tea", "coffee" ya "water" ho sakta hai.

Matlab model sirf random guess nahi karta, balki:
- language rules samajhta hai (grammar).
- meaning samajhta hai (semantics).
- context ko track karta hai.
- long-distance relations samajhta hai.

Yeh sab kaise possible hua?

Yeh sab possible hua ek architecture ki wajah se: ```Transformer```.

<br>

Ab hum aage ek ek step mein samjhenge ki model kaise kaam karta hai.

<br>
<br>

Jab tum kisi LLM ko kuch bhi text input mein dete ho to ye steps follow hote hain.

### Step-1: Tokenization (Text → Tokens):

Is step mein ek sentence ko alag-alag words mein break kiya jata hai.

Token ka matlab hai ek sentence ko chote chote parts mein break karna. Is process ko tokenization kehte hain.

Problem kya hai?

Computer directly text ko samajh nahi sakta:
```
"Hello world"
```
Computer ke liye yeh sirf characters ka sequence hai.

Solution: **Tokenization**

Text ko tod diya jata hai chhote pieces me, Jinko hum tokens kehte hain.

**Example**:

Sentence:
```"ChatGPT is amazing"```.

Tokenization ho sakta hai:
```
["Chat", "G", "PT", " is", " amazing"]
```
Ya:
```
["ChatGPT", " is", " amazing"]
```

<br>

Yeh tokenization kabhi kabhi ese uper jaisea different kyu hota hai?

Kyuki model use karta hai: **Subword tokenization (BPE / WordPiece)**.

Reason:
- New words handle karne ke liye.
- Rare words break karne ke liye.

**Intuition**:

Socho tum English seekh rahe ho:
- Tum words yaad karte ho.
- Lekin agar unknown word aaye:
  - tum usse tod kar samajhte ho

Same LLM bhi karta hai.

<br>
<br>

### Step-2: Token ID Mapping

Is step mein tokens ko ek ID yaani ek number assign kiya jata hai.

**Problem kya hai?**:

Neural networks sirf numbers samajhte hain, text nahi. Toh pehle har word/subword ko ek unique number (ID) dena padta hai.

**Explanation**:

Jab kisi LLM model ko train kiya jata hai to uski training se pehle ek vocabulary banai jaati hai yaani words ki ek dictionary, jisme har unique token ko ek ID assign hoti hai:
```
"hello"  → 15496
"world"  → 995
"!"      → 0
" the"   → 262
```

GPT-2 ki vocabulary mein ~50,000 tokens hain. LLaMA-3 mein ~128,000.

Ye vocabulary har model ki alag hoti hai. Vocabulary se tum ese samjho, Model banane wale engineers pehle:
- Books
- Wikipedia
- Websites
- Code
- Articles

Ye sab lete hain aur Phir decide karte hain:

Kaunse tokens vocabulary mein honge?

To inhi sab chize se words ki ek dictionary banai jaati hai aur un words ko numbers bhi assign kar diye jaate hain.


Vocabulary banne ke baad model train ho gya ab model ko jab input text diya jata hai to model text ko tokens mein break karta hai.

Yahan: 

| Algorithm                    | Used In       | Approach                      |
| ---------------------------- | ------------- | ----------------------------- |
| **BPE** (Byte Pair Encoding) | GPT series    | Frequent pairs merge karo     |
| **WordPiece**                | BERT          | Probability-based merging     |
| **SentencePiece**            | LLaMA, Gemini | Language-agnostic, byte-level |
| **Tiktoken**                 | OpenAI models | Fast BPE implementation       |

Jaise tokenizers use hote hain text ko tokens mein break karne ke liye. Ye tokenizers model ke hisaab se alag-alag ho sakte hain matlab koi model alag tokenizer use kar rha hoga aur koi model dusra tokenizer. Is liye har model ke tokens different ho sakte hain.

Example:

Word:
```
unbelievable
```
Tokenizer:
```
["un", "believ", "able"]
```

Ab text ko tokens mein break karne ke baad step aata hai **Token Id Mapping**. Is step mein vocabulary (dictionary) jo training se pehle create ki gayi thi vo use hoti hai aur Har token ka ID lookup hota hai, matlab vocabulary se token ka id liya jata hai aur token ko id assign kiya jata hai:

Example:

| Token    |   | Token ID |
|----------|---|----------|
| "Hello"  | → | 15496    |
| " world" | → | 995      |
| "!"      | → | 0        |

Final ID list (model ka input)
```
15496  995  0
```

Yeh IDs ek simple integer array hain — yahan tak koi AI nahi, sirf dictionary lookup!


<br>
<br>

### Step-3: Tokens → Numbers (Embedding)

Is step mein token ko ek number assign ya map kiya jata hai, jisko embedding kehte hain.

Problem:
- Computer ko sirf numbers samajh aate hain.

Solution: **Embedding**

Har token ko ek vector (numbers ka list) diya jata hai.

Example:
```
"dog" → [0.2, -0.5, 0.8, 0.1, ...]
"cat" → [0.25, -0.45, 0.75, 0.12, ...]
```

Uper **Token Id Mapping** step mein tokens ko Id assign hui thi, ab is step mein token id ko vector mein convert kiya jata hai.

<br>

**Embedding kya hai?**:

Socho tumhare paas ek shabd hai: "Raja". Computer ko yeh shabd seedha samajh nahi aata, kyunki computer sirf numbers samajhta hai. Toh hume "Raja" ko kuch aise convert karna hoga jisse computer use kar sake.

Embedding basically ek shabd ya sentence ko ek list of numbers mein badal deta hai — jise hum "vector" kehte hain.

Example:
```
"Raja" → [0.9, 0.1, 0.8, 0.2, 0.6, ...] (768 numbers ki list)
"Rani" → [0.9, 0.9, 0.8, 0.8, 0.6, ...] (alag 768 numbers)
"Kutta" → [0.0, 0.0, 0.1, 0.9, 0.1, ...] (bilkul alag numbers)
```

Iska magic yeh hai ki milte-julte matlab wale words ke vectors bhi milte-julte hote hain. "Raja" aur "Rani" ke vectors close hote hain, lekin "Kutta" ka vector dono se door hoga.

<br>

**Embedding kyu zaroori hai?**:

Problem: Text neural network mein directly nahi jaata. Neural networks sirf floating point numbers pe kaam karte hain.

Solution: Har word/token ko ek fixed-size number vector mein convert karo — yahi embedding hai.

<img src="https://drive.google.com/uc?export=view&id=1VjrDyypuiIaGy1LJyt4ImVUx9q0MjNM-" width="620" height="340">

<br>

**Embedding kaise banta hai?**:

Step 1: Tokenization:

Sabse pehle text ko "tokens" mein todte hain. Token ek word bhi ho sakta hai, ya word ka ek hissa bhi.

Example:
```
"Mujhe biryani pasand hai" 
      ↓ Tokenize
["Mujhe", "biryani", "pas", "  and", "hai"]
```

Har token ko ek integer ID milta hai ek lookup table se (vocabulary):
```
"Mujhe"   → 4521
"biryani" → 8873
"pasand"  → 2910
"hai"     → 156
```

Step 2: Embedding Lookup (Token Embedding):

Ab in integer IDs ko asli vectors mein badlo. Is kaam ke liye ek badi matrix hoti hai jise **Embedding Matrix** kehte hain.

Imagine karo ek spreadsheet jisme:
- Rows = vocabulary ke saare words (50,000+ words).
- Columns = embedding dimensions (768 ya 4096).

```
Embedding Matrix (simplified, sirf 4 dimensions dikhaye):
Word       | Dim1  | Dim2  | Dim3  | Dim4
-----------+-------+-------+-------+------
"Raja"     | 0.9   | 0.1   | 0.8   | 0.2
"Rani"     | 0.9   | 0.9   | 0.8   | 0.8
"Kutta"    | 0.0   | 0.0   | 0.1   | 0.9
"Biryani"  | 0.3   | 0.7   | 0.0   | 0.1
```
Jab "Raja" aata hai → ID 4521 → matrix ki 4521vi row nikal lo → yeh hai "Raja" ka embedding!

