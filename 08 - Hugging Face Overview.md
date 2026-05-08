# Hugging Face Overview


### Hugging Face kya hai?

Jaise code ko GitHub par push kiya jata hai. Vaise hi LLM models ko Hugging Face par push kiya jata hai. Hugging face ek tarha se **Github for LLM models** hai.

Jaise code ko host karne ke liye GitHub hai vaise hi LLM models ko host karne ke liye Hugging Face portal hai.

Hugging face ek LLM model hosting platform hai, jaha AI developers apne LLM models ko host karte hain.

Yahan par har tarah ke models train karke push kar diye hain, tum koi bhi LLM model ko download karke apne local system mein usko run kar sakte ho.

**Example**:

Jaise tumne koi LLM model create kiya, ab tum chate ho ki model ko aur log bhi use kar sakte. Isliye tum usko Hugging Face portal par push kar sakte ho. 

Isi tarah se tum koi bhi model use karne ke liye waha se download kar sakte ho.

<br>
<br>

### Hugging Face CLI

Hugging Face khud ki ek CLI provide karta hai jiska use karke tum portal se connect kar sakte ho aur LLM models ko download and run kar skate ho, Aur bhi actions perform kar sakte ho.

The huggingface_hub Python package comes with a built-in CLI called ```hf```. This tool allows you to interact with the Hugging Face Hub directly from a terminal. For example, you can log in to your account, create a repository, upload and download files, etc.

**Install Hugging Face CLI**:

Python Command:
```
pip install -U "huggingface_hub"
```

<br>

**Login to Hugging Hub**:

Warning: `huggingface-cli` is deprecated and no longer works. Use `hf` instead.

Python Command:
```
hf auth login
```

Output:
```
 hf auth login

    _|    _|  _|    _|    _|_|_|    _|_|_|  _|_|_|  _|      _|    _|_|_|      _|_|_|_|    _|_|      _|_|_|  _|_|_|_|
    _|    _|  _|    _|  _|        _|          _|    _|_|    _|  _|            _|        _|    _|  _|        _|
    _|_|_|_|  _|    _|  _|  _|_|  _|  _|_|    _|    _|  _|  _|  _|  _|_|      _|_|_|    _|_|_|_|  _|        _|_|_|
    _|    _|  _|    _|  _|    _|  _|    _|    _|    _|    _|_|  _|    _|      _|        _|    _|  _|        _|
    _|    _|    _|_|      _|_|_|    _|_|_|  _|_|_|  _|      _|    _|_|_|      _|        _|    _|    _|_|_|  _|_|_|_|

    To log in, `huggingface_hub` requires a token generated from https://huggingface.co/settings/tokens .
Token can be pasted using 'Right-Click'.
Enter your token (input will not be visible): 
```

Create a token on Hugging Face hub and paste it on terminal.

After pasting it, the output will be:

Output:
```
Token is valid (permission: write).
The token `Test Token` has been saved to C:\Users\puneetverma02\.cache\huggingface\stored_tokens
Your token has been saved to C:\Users\puneetverma02\.cache\huggingface\token
Login successful.
The current active token is: `Test Token`
```

