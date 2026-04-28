# API Setup and Integration

Ab hum OpenAI aur Gemini ki APIs ko use karke programatically AI LLM models ko use karenge python code ke through. Matlab ChatGPT ya Gemini ko python ke code ke through access karenge, aur in models ke output ko command line par print karayenge.

Normally hum ChatGPT ya Gemini par jakar apni query likhete hain lekin yahan hum python code ke through in models ko apni query bhejenge aur output ko print karayenge.

To OpenAI aur Gemini ne iske liye apni API Key de rakhi hain jise code mein use kiya jata hai.

Iske liye humko LLM models jaise OpenAI ya Gemini ki API Key chaiye hogi jisko hum code ke through access karenge. 

OpenAI ki API Key paid hai, minimum 5$ lagte hain openAI ki API key ko create karke use karne ke liye. Isliye hum Google ke Gemini ki API key use karenge, kyuki Gemini ke API free hai use karna.

<br>

### Gemini API Key

**Step-1: Go to Google AI Studio**:

Go to Google AI Studio, Hit the URL: https://aistudio.google.com/.

**Step-2: Click on Get API Key**:

Click on Get API Key to get the APi Key.

**Step-3: Create a Project**:

Create a project, I created with name: ```Gemini Project Puneet```.

**Step-4: Click on Create API Key**:

Now, Click on Create API Key. Select the project you created.

You will get you api key in a pop-up.

<br>

**My API Key**:

Api Key:
```
AIzaSyBTLN4Z8slwpHZQAzRaOoOO_U6sQiTdRPs
```
Note: Github par API Key commit karne ke baad mujhe google ait studio ne warning ki api ki publically expose ho chuki hai, isliye ye api key ne work karna band kar diya aur code mein error diya tha ki ```api key publically exposed```. Isliye ye api key maine delete kar di thi.

Name:
```
Gemini API Key
```

Project Name:
```
projects/12577051282
```

Project Number:
```
12577051282
```

<br>
<br>

## Access Gemini API Key using Python

Gemini ki API key ko python ke through use karne ke liye ek python library use hoti hai ```google-genai```.

<br>

### Installing Gemini Library:

Library install karne se pehle aap ek virtual environment create kar lijiye. Isse hoga ye ki poore system mein library install nahi hoti, sirf ek particular folder ke ander library install hogi.

**Creating Virtual Environment**:

Commands:
```
# Creating venv named virtual environment
python -m venv .venv

# Activate venv virtual environment
source .venv/bin/activate
```

**Installing google-genai library**:

Command:
```
pip install google-genai
```

<br>
<br>

### Python Code for accessing Gemini API Key

Library install karne ke baad ab python ka code likhte hain jo gemini ke api key ko use karegi gemini LLM model ke output lene ke liye. Isse gemini ka command line mein aayega. Iska matlab hai ki hum gemini ko python ke through use kar rhe hain.

**Create a python file**: ```main.py```

main.py
```
from google import genai

client = genai.Client(api_key="AIzaSyBTLN4Z8slwpHZQAzRaOoOO_U6sQiTdRPs")

response = client.models.generate_content(
    model="gemini-3-flash-preview", contents="Hi, how are you?"
)

print(response.text)
```

Output:
```
I'm doing great, thank you for asking! How are you doing today? Is there anything I can help you with?
```

<br>
<br>

**Note**:

Tutorials mein tutor ne OpenAI ki API Key use ki thi jiski python library alag hai aur code bhi alag hai, To tutor ne kaha ki agar apko OpenAI ke code mein hi gemini ki API Key use karni hai to is tarike se kar sakte hain.

Code to OpenAI ka rahega lekin api key gemini ki hogi aur model bhi gemini use hoga aur request bhi gemini ko jayegi aur output bhi gemini hi dega, bas yaha code library open ai ki use hogi.

<br>

### Install OpenAI Library

Ab openai ki python library install karo:

```
pip install openai
```

<br>

### Python Code for accessing Gemini API Key using OpenAI python code

main.py:
```

```
