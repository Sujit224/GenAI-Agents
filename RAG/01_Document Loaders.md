Loading different kind of documents into your model can be done using Document loaders

```python
! pip install langchain community
```

## 1. Text Loaders

Loading textual data to the model
```python
from langchain_community.document_loaders import TextLoader
text_loader = TextLoader('/content/The Himalayas.txt')
loaded_doc = text_loader.load()
print(loaded_doc)
```

Langchain creates a list to store all the uploaded files 
```python
print(type(loaded_doc))
# Output <class 'list'>
```

---
## 2. PDF Loaders

Loading data from a PDF file into the model
```python
pip install langchain-community pypdf
```

```python
from langchain_community.document_loaders import PyPDFLoader 

pdf_loader = PyPDFLoader('/content/Conics.pdf')
loaded_doc = pdf_loader.load()
print(loaded_doc)
```

Langchain creates a List in which each element is a page of the loaded PDF
```python
print(type(loaded_pdf_doc))
# Output <class 'list'>
```

Length of the loaded_pdf_doc is equal to number of pages in the loaded PDF.
```python
print(len(loaded_pdf_doc))
# Output 32
```

---
## 3. CSV Loader

Loading a CSV file into the document
```python
from langchain_community.document_loaders import CSVLoader  

csv_loader = CSVLoader('/content/Spotify_2024_Global_Streaming_Data.csv')
loaded_csv_doc = csv_loader.load()
print(loaded_csv_doc)
```

```python
print(len(loaded_csv_doc))
# Output 500(no.of rows)
```

---
## 4. Web Loader

```python
from langchain_community.document_loaders import WebBaseLoader
webloader = WebBaseLoader("https://en.wikipedia.org/wiki/Machine_learning")
loaded_web_doc = webloader.load()
print(loaded_web_doc)
```

```python
# Prints the entire content in the web page
print(loaded_web_doc[0])
```

---
