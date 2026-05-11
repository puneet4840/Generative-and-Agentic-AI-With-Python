# Coding Your First AI Agent

Is slide mein hum ek Agent banayenge jo current weather ki information dega.

<br>

**Sabse Pehle**:

Agar hum normally LLM model ko koi real time data puchte hain to vo mostly time real time data nahi deta hai. Kyuki model past data pe trained hua hota hai.

Jaise is example maine LLM model se pucha "What is current weather in goa?"

To LLM model ne result diya 2024 ke data pe.

**Example**:

main.py
```
from openai import OpenAI
from dotenv import load_dotenv
import requests

load_dotenv()

client = OpenAI(
    base_url="https://generativelanguage.googleapis.com/v1beta/openai/"
)

def main():
    user_query = input(">>: ")
    response = client.chat.completions.create(
        model="gemini-3-flash-preview", 
        messages=[
            {"role": "user", "content": user_query}
        ]
    )

    print(f"BOT:{response.choices[0].message.content}")


main()

```

Output:
```
BOT:As of June 10, 2024, Goa is currently entering the **monsoon season**. Here is a breakdown of the current weather conditions:

*   **Temperature:** Highs of around **31°C (88°F)** and lows of **26°C (79°F)**.
*   **Conditions:** Generally cloudy with a high probability of **intermittent rain and thunderstorms**. The monsoon has officially arrived in the region, so expect sudden, heavy downpours followed by humid, overcast periods.
*   **Humidity:** Very high, typically between **80% and 90%**, which makes it feel warmer than the actual temperature.
*   **Sea Conditions:** The sea is rough, and swimming is generally prohibited at most beaches due to strong currents and high tides during the monsoon.
```

Ye LLM model ne response diya. To ye response LLM model ne old data ke hisab se diya jis data pe ye model train hua hai.

Iska matlab LLM model real time data ko nhi deta hai.

Ye to baat thi vo LLM model jo API call se use kiya. Maine khud se ye prompt ChatGPT ko diya aur usne searching the web karne baad real data ka response diya. Iska matlab ChatGPT kisi weather api ko alag se call kar rha hai aur data collect karke response de rha hai.

<br>

### Getting weather data from weather api

Maine alag se ek python function create kiya jo ek api ko call kar rha hai aur city ka input dene par us city ka weather response mein bhej rha hai. Maine ye function isliye create kiya kyuki mai ye check kar saku ki api call se weather ki information kaise aati hai.

get_weather.py
```
def get_weather(city):
    url = f"https://wttr.in/{city.lower()}?format=%C+%t"
    response = requests.get(url)

    if response.status_code == 200:
        return f"The current weather in {city} is: {response.text}"
    
    return f"sorry, I couldn't fetch the weather for {city} right now."

print(get_weather("Dibai"))
```

Output:
```
The current weather in Dibai is: Clear +34°C
```

Ye output aaya weather api call karne ke baad.

<br>

Ab ek Agent banane ke liye hum LLM model ko is ```get_weather``` function ka context denge aur LLM model weather details fetch karne ke liye is ```get_weather``` function ka use karega.

<br>
<br>

### Complete Code of Weather Agent

main.py:
```
from openai import OpenAI
from dotenv import load_dotenv
import requests
import json

load_dotenv()

client = OpenAI(
    base_url="https://generativelanguage.googleapis.com/v1beta/openai/"
)

def get_weather(city):
    url = f"https://wttr.in/{city.lower()}?format=%C+%t"
    response = requests.get(url)

    if response.status_code == 200:
        return f"The current weather in {city} is: {response.text}"
    
    return f"sorry, I couldn't fetch the weather for {city} right now."





Sytem_Prompt = """
You are an expert Ai Assistant in resolving user queries using Chain of Thought prompting technique. You will be given a question and you have to break down the question into multiple steps and then answer the question.

You work on START, PLAN and OUTPUT steps.

You can also use the get_weather function to fetch the current weather of any city. Just call the function with the city name as argument and it will return the current weather of that city.

Available function:
get_weather(city) - This function takes the name of the city as input and returns the current weather of that city.

Example-1:
Question: If there are 3 cars and each car has 4 wheels, how many wheels are there in total?
START: I will first calculate the number of wheels in one car and then multiply it by the number of cars.
PLAN: Number of wheels in one car = 4
Number of cars = 3
OUTPUT: Total number of wheels = Number of wheels in one car * Number of cars = 4 * 3 = 12

Example-2:
Question: What is the current weather in Delhi?
START: I will use the get_weather function to fetch the current weather in Delhi.
PLAN: Calling get_weather("Delhi") function to get the current weather in Delhi.
OUTPUT: The current weather in Delhi is: Partly cloudy +30°C.

"""

message_history = []
message_history.append({"role": "system", "content": Sytem_Prompt})

user_query = input(">>: ")
message_history.append({"role": "user", "content": user_query})


while True:
    response = client.chat.completions.create(
        model="gemini-3-flash-preview", 
        response_format={"type": "json_object"},
        messages=message_history
    )

    raw_results = response.choices[0].message.content
    message_history.append({"role": "assistant", "content": raw_results})

    parsed_results = json.loads(raw_results)

    if parsed_results.get("step") == "START":
        print ("LLM Started...", parsed_results.get("content"))
        continue

    if parsed_results.get("step") == "PLAN":
        print ("REASONING...", parsed_results.get("content"))
        continue

    if parsed_results.get("step") == "OUTPUT":
        print ("BOT: ", parsed_results.get("content"))
        break

```

Ab LLM model ```get_weather``` function ko call karke weather ki information lega aur output mein hum dikhayega.

This is your small AI Agent.
