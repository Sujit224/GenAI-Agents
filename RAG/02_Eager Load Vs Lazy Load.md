In LangChain, **eager loading** refers to using the `load()` method to fetch all documents into memory at once, while **lazy loading** uses the `lazy_load()` method (a generator) to yield documents one at a time, only when needed.

Code

Eager Loading
```python
from langchain_community.document_loaders import PyPDFLoader 

pdf_loader = PyPDFLoader('/content/Conics.pdf')
loaded_doc = pdf_loader.load()
print(loaded_doc)
```


Lazy Loading
```python
lazy_loaded_pdf_doc = pdfloader.lazy_load()
for doc in lazy_loaded_pdf_doc:
	print(doc)
```
