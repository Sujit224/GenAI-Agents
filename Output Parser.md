We can organize the output of an LLM though it does not have the structured output feature using Output parser.

### 1. StrOutputParser

```python
from langchain_core.output_parsers import StrOutputParser
```

Create a Parser and pass it int the chain. Now you need not print (result.content)
The output is now automatically parsed.
```python
parser = StrOutputParser()
chain_example = prompt_template_with_message | model |parser
result = chain_example.invoke({"language":"python","error":"Indentation(spacing)"})
print(result)
```

### 2. JSON Output Parser
