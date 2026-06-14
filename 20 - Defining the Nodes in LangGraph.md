# Defining the nodes in LangGraph

Node is simply a function that does a task.

LangGraph mein node ek function hota hai jo kuch task perform karta hai. To hum nodes create karenge.

Folder Structure:
```
LangGraph
|- chat.py
```

```chat.py```:
```
#Nodes

def chatbot(state: State):
    return {"message": ["Hey This message is from chatbot node."]}


def sample_node(state: State):
    return {"message": ["Sample message appended."]}


graph_builder = StateGraph(State)

#Adding nodes to the graph

graph_builder.add_node("chatbot", chatbot)
graph_builder.add_node("sample_node", sample_node)
```

<br>

### Complete Code

```chat.py```:
```
from typing import Annotated, TypedDict
from langgraph.graph import StateGraph, START, END
from langgraph.graph.message import add_messages

class State(TypedDict):
    # Define messages (a list type, with the add_messages function used to append messages)
    messages: Annotated[list, add_messages]


#Nodes

def chatbot(state: State):
    return {"message": ["Hey This message is from chatbot node."]}


def sample_node(state: State):
    return {"message": ["Sample message appended."]}


graph_builder = StateGraph(State)

#Adding nodes to the graph

graph_builder.add_node("chatbot", chatbot)
graph_builder.add_node("sample_node", sample_node)
```

Explanation:
```
# state = {"message": ["Hey There!"]}
# node runs chatbot(state: ["Hey There!"]) --> returns ["Hey This message is from chatbot node."]
# state = {"message": ["Hey There!", "Hey This message is from chatbot node."]}
```
