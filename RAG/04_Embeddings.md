An **embedding** is ==a way to represent complex data (like words, images, or user actions) as dense numerical vectors (lists of numbers) that capture their meaning and relationships==, allowing AI/ML models to process them efficiently for tasks like search, recommendations, and understanding context. Similar items have similar vectors, placing them closer in a multi-dimensional "embedding space," revealing patterns that raw data hides, making AI smarter


### Code Implementation
```python
from langchain_google_genai import GoogleGenerativeAIEmbeddings

embeddings = GoogleGenerativeAIEmbeddings(model='gemini-embedding-001',google_api_key=API_KEY)
```

We use Chroma as a Vectore_Store to store our embeddings
```python
pip install -qU "langchain-chroma>=0.1.2"
```

```python
from langchain_chroma import Chroma
vector_store = Chroma.from_texts(res,embeddings)
# Here res = Text splitted output recieved on using a text splitter
```

```python
vector_index = vector_store.as_retriever(search_kwargs={'k':5})
# search_kwargs = No.of results to return
```


