Building a Crew AI Agent

```python
!pip install crewai
```

### Setting your LLM in CrewAI
```python
pip install -U litellm
from crewai import LLM
```

```python 
llm = LLM(
    model="llama-3.1-8b-instant",
    temperature=0.3,
    api_key=OPENAI_API_KEY
)
```

### Building the Agent

```python
from crewai import Agent,Task,Crew  

agent = Agent(
    role="Motivational Speaker",
    goal = "Create an inspirational LinkedIn post for job seekers",
    backstory = "An experienced carrer mentor who inspires others through writing.",
    llm = llm
)
```

```python
task = Task(

    description = "Write a short LinkedIn post to motivate job seekers",
    expected_output="Clean ans humanised LinkedIn post",
    agent = agent # Specifying the agent that is supposed to perform this task
)
```

```python
crew = Crew(

    agents = [agent], # List of all agents created
    tasks = [task] # List of all tasks created
)
```

```python
print(crew.kickoff())
```

### Giving Input during the Runtime
```python
agent1 = Agent
    role="Motivational Speaker",
    goal = "Create an inspirational LinkedIn post for job seekers",
    backstory = "An experienced carrer mentor who inspires others through writing.",
    llm = llm
)
```

```python
task1 = Task(
    description = "Write a short LinkedIn post to motivate job seekers on topic = {topic}",
    expected_output="Clean ans humanised LinkedIn post",
    agent = agent1 # Specifying the agent that is supposed to perform this task
)
```

```python
crew1 = Crew(
    agents = [agent1], # List of all agents created
    tasks = [task1] # List of all tasks created
)
```

```python
print(crew1.kickoff(inputs = {"topic" : "Data Scientists"}))
```
