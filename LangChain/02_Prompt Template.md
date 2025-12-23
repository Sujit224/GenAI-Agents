You can use templates for standard prompts by just changing few variables during run time.

## Method1
Import statement
```python
from langchain_core.prompts import ChatPromptTemplate
```

```python
query = "I am preparing for DSA interviews ans practising questions. You are an experienced {language} developer. Help me with the error {error}"
prompt = ChatPromptTemplate.from_template(query)

prompt_value = prompt.invoke({"language":"python","error":"Indentation(spacing)"})
result = model.invoke(prompt_value)
print(result.content)
```

### Prompt template with Users

```python
template_message = [
    ("system","You are an experienced {language} developer"),

    ("human","I am preparing for DSA interviews ans practising questions. Help me with the error {error}")
]
```

```python
prompt_template_with_message = ChatPromptTemplate.from_messages(template_message)
prompt_input = prompt_template_with_message.invoke({"language":"python","error":"Indentation(spacing)"})

response = model.invoke(prompt_input)
print(response.content)
```

## 🔗Chaining in LangChain

> [!NOTE]
> A detailed discussion on Chains is made in the upcoming chapters. Now Chains are only discussed to get familiar with the second method.

```python
template_message = [
    ("system","You are an experienced {language} developer"),

    ("human","I am preparing for DSA interviews ans practising questions. Help me with the error {error}")
]

prompt_template_with_message = ChatPromptTemplate.from_messages(template_message)
chain_example = prompt_template_with_message | model 

result = chain_example.invoke({"language":"python","error":"Indentation(spacing)"})
print(result.content)
```

---
## Method 2

> [!NOTE] Partial Variables
> This method makes use of Partial Variables which will be discussed in detail under Output Parser.

```python
from langchain_core.prompts import PromptTemplate
```

```python
prompt_template = PromptTemplate(
    template="Help me resolve error {error}. Explain to a {age} old person",
    input_variables=["error"],
    partial_variables={'age':'3'}
)
```

With Chaining
```python
chain = prompt_template | model
result = chain.invoke({"error":"var is not defined"})
print(result.content)
```

Without Chaining
```python
prompt_value = prompt_template.invoke({"error":"Indentation is missing"})
result = model.invoke(prompt_value)
print(result.content)
```

