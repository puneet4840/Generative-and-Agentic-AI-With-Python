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

### Step-2: Tokens → Numbers (Embedding)

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
