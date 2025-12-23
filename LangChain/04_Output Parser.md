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

Creating a JSON output Parser
```python
from langchain_core.output_parsers import JsonOutputParser
json_parser = JsonOutputParser()
```

```python
from langchain_core.prompts import PromptTemplate  

prompt_template_with_json_parser = PromptTemplate(
  template="Help me resolve error {error}.Format = {format_instructions}",
  input_variables=["error"],
  partial_variables={'format_instructions':json_parser.get_format_instructions()}
)
print(prompt_template_with_json_parser)
```
###### With Chain
```python
chain_with_json_parser = prompt_template_with_json_parser | model | json_parser
result = chain_with_json_parser.invoke({"error":"Missing attribute name"})
print(result)
```

###### Without Chain
```python
# Without the Chain

chain_without_json_parser1 = prompt_template_with_json_parser | model #We have not passed the Parser in the chain

result = chain_without_json_parser1.invoke({"error":"Missing attribute name"})
print(result)
```

In both the cases you get a JSON Parsed output but however the LLM adds its own property names to the JSON response.
If you want to customize then you must make use of the Structures Output method.

### 3. Using Pydantic

```python
class ErrorResolution(BaseModel):

  fix:str = Field(description="Process or steps to fix the error or actual resolution")

  cause: str = Field(description="Cause of the error")
```

```python
from langchain_core.output_parsers import PydanticOutputParser

pydantic_parser = PydanticOutputParser(pydantic_object=ErrorResolution)
```

```python
prompt_template_with_pydantic_parser = PromptTemplate(
  template="Help me resolve error {error}.Format = {format_instructions}",
  input_variables=["error"],
  partial_variables={'format_instructions':pydantic_parser.get_format_instructions()}
)

print(prompt_template_with_pydantic_parser)
```

```python
pydantic_parser_chain = prompt_template_with_pydantic_parser | model | pydantic_parser

result = pydantic_parser_chain.invoke({"error":"Indentation error"})
print(result)
```
