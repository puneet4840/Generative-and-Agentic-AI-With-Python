# Implementing a Custom Tokenizer in Python

Is slide mein hum ek custom tokenizer create karege python ki help se.

We know that ki LLM mein first step hote a text ko tokens mein break karna, to vo progmatically hota kaise hai vo hum dekhnge.

<br>

Agr apko dekhna hai ki sentence tokens mein kaise break hota hai, iske liye ek website hai ```Tiktokenizer``` https://tiktokenizer.vercel.app/ 

Ispe aap dekh sakte ho sentence tokens mein kaise break hota hai.

<br>
<br>

### Step-1: Install Tiktoken Library

```
pip install tiktoken
```

<br>

### Step-2: Write apython code for Tokenization:

Code:
```
import tiktoken

enc = tiktoken.encoding_for_model("gpt-4o")

text="Hey There!, My name is Puneet"

tokens = enc.encode(text)

print(tokens)
```

Output:
```
[25216, 3274, 27942, 3673, 1308, 382, 102208, 292]
```

<br>

### Step-3: Write python code for detokenization:

Code:
```
de_tokens = enc.decode(tokens)

print(de_tokens)
```

Output:
```
Hey There!, My name is Puneet
```

<br>

### Complete Code

```
import tiktoken

enc = tiktoken.encoding_for_model("gpt-4o")

text="Hey There!, My name is Puneet"

tokens = enc.encode(text)

print(tokens)

de_tokens = enc.decode(tokens)

print(de_tokens)
```


