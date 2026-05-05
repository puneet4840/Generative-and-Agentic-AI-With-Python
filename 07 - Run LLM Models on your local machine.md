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

**How Ollama works**:

```
┌──────────────┐         ┌──────────────────┐         ┌──────────────┐
│              │  HTTP    │                  │  Inference│             │
│  Open WebUI  │────────▶│  Provider API    │────────▶ │    Model     │
│  (frontend)  │◀────────│  (cloud/local)   │◀──────── │  (LLM/VLM)  │
│              │  Stream  │                  │  Tokens  │             │
└──────────────┘         └──────────────────┘         └──────────────┘
```
- You type a message in Open WebUI.
- Open WebUI sends it to your provider's API endpoint.
- The provider runs inference on the selected model.
- Tokens stream back to Open WebUI in real time.
- You see the response in the chat interface

<br>

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
```
docker run -d -v ollama:/root/.ollama -p 11434:11434 --name ollama ollama/ollama
```

This command will download the ollama docker image and run the docker container.

**Step-2: Check contianer in running**:

```
docker ps
```
output:
```
CONTAINER ID   IMAGE           COMMAND               CREATED         STATUS         PORTS                                           NAMES
587f77a192e2   ollama/ollama   "/bin/ollama serve"   5 minutes ago   Up 5 minutes   0.0.0.0:11434->11434/tcp, :::11434->11434/tcp   ollama
```
Access:
```
http://localhost:11434
```

Humne ollama container to run kar diya ab prompt kaha dena hai model ko. Yahan use hota hi ```OpenWeb UI``` tool. Ye ollama ke liye ek UI layer hoti hai, jo ollama se interact karti hai, Isi ```OpenWeb UI``` ke through hi hum prompt dete hain ollama container ko.

**Step-3: Pull the OpenWeb UI container image**:
```
docker pull ghcr.io/open-webui/open-webui:main
```

**Step-4: Run the OpenWeb UI container**:
```
docker run -d -p 3000:8080 --add-host=host.docker.internal:host-gateway -v open-webui:/app/backend/data -e OLLAMA_BASE_URL=http://host.docker.internal:11434 --name open-webui ghcr.io/open-webui/open-webui:main
```
Access:
```
http://localhost:3000
```

```docker run``` command chalane ke 2 se 3 minutes baad Ab OpenWeb UI container bhi run ho rha hai.

```OpenWeb UI``` automatically ollama container ke saath connect ho jata hai.

Ab tum apne prompts OpenWeb UI mein LLM model ko doge.

<br>
<br>

### Pull the LLM model to OpenWeb UI

Ab ollama aur OpenWeb UI dono run ho rahe hain. Ab hum open source LLM model OpenWeb UI mein add karna hoga. Add karne par model OpenWeb UI mein add ho jayega.

Step to add:
```
Step-1: Go to Admin Panel.
Step-2: Click on Settings.
Step-3: Click on models.
Step-4: Click on manage.

A pop will occur with the ollama.
```

Enter the model name ```gemma:2b``` at ```Pull a model from ollama.com``` and hit download button next to it.

Tumhare ```gemma:2b``` model download hona start ho jayega.

Download hone ke baad tum ```Admin Panel``` -> ```Setting``` -> ```Models``` mein jake apna model dekh sakte ho.

<br>
<br>

### Use your model

Ab tum apna model use kar sakte ho.

Go to OpenWeb UI homepage. Select your model from dropdown.

Give the prompt to your model.

<br>

<img src="https://drive.google.com/uc?export=view&id=15Qwz68xo9-sLzH4_W-F5ksxIIqF54-yI" width="600" height="350">

<br>

LLM model bohot jyada CPU aur Memory use karta hai. Aur ollama in model ko run kar rha hai. To mere local system ke CPU aur Memory consumption kitna high chla gya tha.

<img src="https://drive.google.com/uc?export=view&id=1lVpl3Q-uubaxO2o_bLONCQup-kZb9bM9" width="600" height="40">

Is tarike se tum LLM models ko apne local systems mein use kar sakte ho.

<br>
<br>
<br>

## Access the LLM model using the Python code

Abhi tak hum OpenWeb UI ke through apne prompt LLM model ko de rhe the, Lekin ab hum python code ke through apne prompt Ollma se chal rhe LLM model ko denge.

### Step-1: Install the Libraries

Sabse pehle ye libraries install karni hain:
```
pip install "fastapi[standard]"
pip install ollama
```

<br>

### Step-2: Create a python file

```server.py```
```
from fastapi import FastAPI, Body
from ollama import Client

app = FastAPI()

client = Client(
    host="http://localhost:11434",)


@app.get("/")
def read_root():
    return {"Hello": "World"}

@app.post("/chat")
def chat(
        
        message: str = Body(..., example="What is the capital of France?")
):
    response = client.chat(model="gemma:2b", messages=[{"role": "user", "content": message}])

    return {"response": response.message.content}
```

<br>

### Step-3: Run python file

Ab python file ko run karo.

command:
```
fastapi dev server.py
```

Tumhara fastapi ka server run ho jayega.

**Access your app**:

Ab browser mein ```http://127.0.0.1:8000/``` hit karo tumhara fastapi app tumko dekhega. 

Fastapi swagger ui bhi deta hain jisse aap apne api test kar sakte ho. To swagger access karne ke liye ye url browser mein hit kar ```http://127.0.0.1:8000/docs```.

Isse swagger ka ui open ho jayega jaha tumhara ```/chat``` post method bhi dikhega.

Try it out pe click karke value mein apni query likhiye aur execute kar do. LLM model ke paas request jayegi aur model response de dega.

<br>

<img src="https://drive.google.com/uc?export=view&id=1rgam-vKfgjN7u-aD_RzGi9_Rdmcd2msO" width="800" height="530">

<br>

DONE!!!
