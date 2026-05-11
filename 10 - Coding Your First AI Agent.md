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

