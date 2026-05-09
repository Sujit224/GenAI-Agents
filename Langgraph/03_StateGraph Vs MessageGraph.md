
In LangGraph, the type of graph you choose determines how you manage the "memory" or data flow between nodes.

| Feature | StateGraph | MessageGraph |
| :--- | :--- | :--- |
| **Definition** | A general-purpose graph where **you define the schema** (the "State"). | A specialized subclass of StateGraph where the schema is **pre-defined**. |
| **The State** | Fully customizable (e.g., a `TypedDict` or Pydantic model containing keys for *documents*, *iterations*, *user_info*, etc.). | Restricted specifically to a **list of messages** (`Sequence[BaseMessage]`). |
| **Data Flow** | Nodes accept the custom state and return updates to specific keys. | Nodes accept the list of messages and usually return a new message to append. |
| **Best For** | Complex RAG flows, agents needing structured outputs, or workflows tracking multiple distinct variables. | Simple chatbots or conversational agents where context is just the chat history. |

---
## Code

```python
from langgraph.graph import StateGraph
from typing import TypedDict
```

Creating your Custom Dictionary
```python
class MyState(TypedDict):
  count : int
```

```python
graph = StateGraph(MyState)
  

def increment_node(state):
  state["count"] = state["count"]+1
  return state
  
graph.add_node("Increment",increment_node)
graph.set_entry_point("Increment")

def isCountReachedLimit(state):
  if state["count"]>=8:
    return END

  else:
    return "Increment"  

graph.add_conditional_edges("Increment",isCountReachedLimit)
```

