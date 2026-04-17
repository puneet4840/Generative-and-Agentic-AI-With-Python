# Understaning LL (Large Language Model)

### LLM (Large Language Model) kya hai?

LLM (Large Language Model) ek AI model hai jo human language ko samjta hai aur generate karta hai.

Ye ek AI model hota hai jo human language ko samajh bhi sakta hai aur generate bhi kar sakta hai. 

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

Ye paper kehta tha ki ```Ek word ko sentence ke ander other words par relation rakhe```.

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

