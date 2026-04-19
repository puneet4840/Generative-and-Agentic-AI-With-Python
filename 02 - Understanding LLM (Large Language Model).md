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


