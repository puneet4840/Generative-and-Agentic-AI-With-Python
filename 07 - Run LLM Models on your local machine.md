# Run LLM Models on your local machine

Abhi tak hum closed source LLM models ko use kar rhe the jaise OpenAI ka ChatGPT, Google ka Gemini, Anthropic ka Claude. To ye models closed source models hain jo in companies ke khud ke infrastruture par run ho rahe hain. Closed Source ka matlab ki in models ko aap apne local machine par run nahi kar sakte. 

In models ko ye companies own karti hain aur ye publically available nahi hain.

Hum in models ko sirf use kar sakte hain lekin khud ke local machine par run nahi kar sakte. Kyuki inka source code aur training data sab hidden hota hai.

To in models jaise ChatGPT, Gemini aur Claude ko use karne ke liye inki API ke through use kar sakte hain. Aur inki API ko use karne ke liye ye compamies charge karti hain.

Lekin kuch ese bhi open source LLM models hain jinko hum apne local machine par use kar sakte hain. Jaise **DeepSeek-R1**, **Qwen3**, **Llama3.3**, **Gemma3** aur other models. Ye open source models hain. In models ko download karke apne local machine par use kar sakte hain.

Lekin ek LLM model ko locally run karne ke liye High CPU aur Memory chaiye hoti hai to ek high configuration system par hi locally run karna chaiye.

To in models ko locally run karne ke liye ek tool hota hai **Ollama**.

<br>
<br>

### What is Ollama?

Ollama ek open-source tool hai jo LLM models ko locally (Windows, Linxu aur MacOS) par run karne ke liye banaya gaya hai.

There are two methods to run Ollama on your local machine:

**Method-1**:

Directly download the Ollama setup(.exe) from internet and run.

Lekin ese download karke run karne par problem hai, Ye setup ek to platform independent hain matlab Linux, Windows aur MacOS par alag alag download karna padta hai. Dusra ye tumhare system ko bloat kar deta hai matlab kaafi space consume karta hai.

<br>

**Method-2**:


Run Ollama as a docker container.

Dusra option hai Ollama ko as a docker container run karna. Ye ek accha method hai kuki isme koi setup download aur install nhi karna hota, sirf container image download karke run karni hoti hai, jo itna space consume nahi karti.

Dusra ki docker container platform independent hai. Isko kisi bhi platform par as a docker container run kar sakte hain.

<br>
<br>

### Run Ollama as a Docker Container on Linux

**Step-1: Run the below command to spin up the docker container on linux**:
