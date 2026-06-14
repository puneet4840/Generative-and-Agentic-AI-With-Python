# Defining the state in LangGrpah

Is slide mein hum LangGraph ke through AI agent ke liye ek state define karenge, jise nodes used karenge.

State ek shared memory hoti hai jisko nodes use karte hain aur ek-dusre ko paas karte hain.

<br>

Folder Struture:
```
LangGraph
|- chat.py
```

```chat.py```:
```
from typing import Annotated, TypedDict
from langgraph.graph import StateGraph, START, END
from langgraph.graph.message import add_messages

class State(TypedDict):
    # Define messages (a list type, with the add_messages function used to append messages)
    messages: Annotated[list, add_messages]


graph_builder = StateGraph(State)
```
