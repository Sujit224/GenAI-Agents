## 🦜🔗 Intro to LangChain

> [!ABSTRACT] The "Operating System" for LLMs **LangChain** is a framework that lets you build applications powered by Language Models. It turns an LLM from a text-generator into a **cognitive engine** that can connect to your data and interact with the world.
> 
> **Core Philosophy:** _Composability_. Building complex apps by chaining simple, modular blocks together.

### ❓ Why use it?

You _could_ just call the OpenAI API directly. But LangChain solves the "messy" parts of engineering:

1. **Abstraction:** Switch from OpenAI to Anthropic or Llama 2 by changing one line of code.    
2. **Context Management:** It handles chunking large PDFs and managing chat history window sizes automatically.    
3. **Reasoning:** It provides the architecture (Agents) for the AI to "think" before it acts.


Invoking LangChain into your notebook
```python
! pip install -qU langchain-google-genai
```

Calling the Gemini model directly from LangChain without using Gemini Docs.
Thus LangChain makes it very smooth for us to access the API of an LLM abstracting all the complex procedures. 

```python
from langchain_google_genai import ChatGoogleGenerativeAI
model = ChatGoogleGenerativeAI(model="gemini-2.5-flash",api_key = API_KEY)
response = model.invoke("What is Animal Planet")
```

## Users in LangChain

Now the model directly gives you output in one word "Bhubaneshwar" directly as it is trained with Human and AI messages of questions in the same format.
```python
messages = [
    SystemMessage(content="Keep the tone polite and the information factual in one word"),
    HumanMessage(content="What is the capital of Karnataka"),
    AIMessage(content="Bengaluru"),
    HumanMessage(content="What is the capital of Odisha?")
]

result=model.invoke(messages)
print(result.content)
```
