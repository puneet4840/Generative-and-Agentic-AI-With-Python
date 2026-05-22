# Problems with the RAG we implemented.

Pehle ki slides mein humne ek simple RAG implement kiya. Humne kuch python files create aur unko run kiya aur RAG run ho kya, Lekin us code implementation mein ek problem hai.

Promblem ye hai ki vo code Synchronous hai. 

Matlab abhi hum sirf ek PDF file ko RAG ke throgh process kar rahe hain, jab hum indexing python code run karte hain aur to indexing phase 1 pdf file ko process karne mein kam se kam
10 se 20 seconds leta hai aur terminal busy rehta hai jab tak code complete finish na ho jaye.

Agar yahi hum indexing code ko 100 se 200 pdf file de de process karne ke liye to ye code bohot jyada time laga lega aur terminal kaafi time tak busy rahega. Isi ko synchronous bolte hain.

Jo ki production mein ese chize work nhi karti hain.

Production mein chize Asynchronous hoti hain. Matlab code apna kaam karta rahega aur user apni query code ko deta rahega.

**Sync**: It waits until the process is completed.

**Async**: Lets do this in background and let user do whatever he wants.

To hum RAG code ko Synchronous se Asynchronous banyenge.

<br>
<br>

### Converting RAG code to Asynchronous

Ab hum Queue system design ka use karenge code ko Synchronous se Asynchronous mein convert karne ke liye.

Hum kya karenge ki suppose hum ek FastAPI ka server banyenge, jo user ki request ko recieve karega. Fir user ki request ek queue mein bhejenge, Fir queue ke dusre end par ek 
function hoga ho request ko procees karega aur response generate karega aur response ko ek DB mein store karega.

Fir agar user ko apni query ka response chaiye to direct Database se user ki query ka response return kar denge.

<br>

**Pehle Kya ho rha tha**:

Suppose tumne ek python Fast API ke server run kar rkha hai, ek user aaya usne apni query server ko bheji ```What is NodeJS?```. RAG code to Sync structure par based hai. To server user ki query ka response generate karne ke liye busy ho jayega.

Itni der mein dusra user aa gya aur query karne laga to server pehle user ki query process karne mein busy hai to dusre user ko server busy milega.

Jo ki ek best practise nhi hai.

Hum is problem ko solve karenge code ko Asynchronous structure mein convert karke.

<br>

**Problem kaise solve hui**:

Humne code ko Asynchronous structure mein convert kar diya. TO jab bhi user server ko apni query bhejega to server us query ko queue mein daal dega aur free ho jayega. 

AB agar bohot saare users aaye aur server ko request karne lage to server sabhi users ki query ko queue mein daal dega aur free ho jayega. Queue ke dusre end par ek alag code work kar rha hoga aur queries ko process karke db mein response store karta jayega.

Ese ye system Asychronous behave karega.

<br>
<br>

### Setting up the Things

Queue ko setup karne ke liye hum Python ki ek library **Python RQ** ka use karenge. Ye library background mein redis ka use karti hai, lekin redis ne open-source license revoke kar diya hai. Normally aap abhi bhi Redis ko apne local system par Docker ke jariye bilkul free aur normally use kar sakte hain.

Yeh restriction sirf un badi cloud companies (jaise AWS) ke liye hai jo Redis ko bechkar apna khud ka paid service chalati hain.

To hum redis na use karke **Valkey** ka use karenge, Valkey bilkul same redis ki tarah hi work karti hai.

<br>

**Install the python RQ library**:
```
pip install rq
```
Ye library python code ko redis queue ke saath work karne ke liye use hogi. Filhal hum valkey use kar rahe hain, lekin code mein redis ka use karenge. To redis ke code ke saath valkey queue perfectly work karti hai.

<br>
<br>

**Create Directory Structure**:

Ye directory structure create karlo:
```
/RAG_with_enhancements
  |- /client
      |- rq_client.py
  |- /queues
      |- 
  |- docker-compose.yml
```

<br>
<br>

**Run the valkey and qdrant containers**:

Create a docker-compose yaml file and write the below configuration in it.

```docker-compose.yml```:
```
services:
  valkey:
    image: valkey/valkey
    container_name: valkey
    ports:
      - "6379:6379"

  vector-db:
    image: qdrant/qdrant:latest
    container_name: vector-db
    ports:
      - "6333:6333"
```
Run the container:
```
docker compose up -d
```
Isse valkey aur qdrant container port 6379 aur 6333 par run ho jayenge.


