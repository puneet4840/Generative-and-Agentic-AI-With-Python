# What is MultiModal AI?

Multi Modal AI ese AI models hote hain jo ek time par multiple types ke data ko samjh sakte hain. 

Jaise kuch models ese hote hain jo sirf text hi input lete hain aur text hi output mein dete hain. Lekin Multi-modal ai models text ke saath saath image, video audio, voice, documents 
jaise data ko input lete hain aur process karte hain.

<br>

Aisi AI jo sirf text hi nahi, balki image, audio, video, voice, documents, aur kabhi-kabhi sensor data bhi samajh sake.

Multimodal AI ek aisi AI technology hoti hai jo ek hi time par multiple types ke data ko samajh sakti hai, process kar sakti hai, aur combine karke intelligent response de sakti hai.

<br>
<br>

### Traditional AI

Purani AI models usually sirf ek type ka data handle karti thi. Jo models shuru mein introduce hue the vo itne advance nhi hote the, sirf ek baar mein ek type data ko hi samjhte the aur process karte the.

Example:
- Chatbot → sirf text.
- Speech recognition → sirf audio.
- Image classifier → sirf image.

Agar tum image bhejo text chatbot ko, vo samajh nahi payega.

<br>

### Multimodal AI

Multimodal AI multiple inputs ko combine karti hai. Aajkl naye AI models multi-modal hain.

Example:

Tum AI ko:
- ek photo bhejo.
- saath mein text question pucho.
- voice mein explain karo.

Aur AI tino ko combine karke answer degi.

Jaise:
- Image dekhegi.
- Voice ko text mein convert karegi.
- Context samjhegi.
- Final intelligent response degi.

Yahi multimodal AI hai.


<br>
<br>

## Implementing Multi-modal AI using gemini model

Is implementation mein hum ek website se image ka url copy karke model ko denge aur model us image ko text form mein explain karega ki exactly image kya hai.

Mai ```pexels.com``` website par gaya aur wha se ek image ki url copy karli aur model ko dedi.

```main.py```:
```
from openai import OpenAI

client = OpenAI(
    api_key="XXXX",
    base_url="https://generativelanguage.googleapis.com/v1beta/openai/"
)



response = client.chat.completions.create(
        model="gemini-3-flash-preview", 
        messages=[
            {"role": "user", "content": [{"type": "text", "text": "Generate a caption for this image in about 50 words."}, 
            {"type": "image_url", "image_url": {"url": "https://images.pexels.com/photos/7988116/pexels-photo-7988116.jpeg"}}]}
        ]
    )


print(response.choices[0].message.content)
```

Output:
```
Two software developers work diligently in a modern, brightly lit office. Seated in ergonomic chairs, they focus intensely on multiple monitors displaying complex code. The clean workspace, complete with a lush green plant and minimalist wall art, reflects a professional and productive atmosphere where technology and innovation meet.
```
