# Agentic_AI
# 📚 LangChain RAG Project (Google Colab)

This project demonstrates a simple **Retrieval-Augmented Generation (RAG)** pipeline using **LangChain**, **OpenAI**, and **FAISS** in Google Colab.

It loads text data, converts it into embeddings, stores it in a vector database, and allows users to query the data using an LLM.

---

## 🚀 Features

* Load and process text documents
* Split large text into smaller chunks
* Generate embeddings using OpenAI
* Store embeddings in FAISS vector database
* Retrieve relevant context based on user query
* Generate answers using LLM (Chat model)

---

## 🧠 Architecture Flow


```mermaid
flowchart LR
    A[📄 Load Data] --> B[✂️ Split Text]
    B --> C[🔢 Generate Embeddings]
    C --> D[🗂 Store in FAISS]
    D --> E[🔍 Retrieve Context]
    E --> F[🧠 LLM (ChatOpenAI)]
    F --> G[✅ Final Output]
```

---

## 📂 Project Structure

```
.
├── data.txt                # Input text file
├── notebook.ipynb         # Google Colab notebook
├── README.md              # Project documentation
└── .env                   # Environment variables (API key)
```

---

## ⚙️ Installation & Setup

### 1. Clone Repository

```bash
git clone https://github.com/your-username/langchain-rag-project.git
cd langchain-rag-project
```

---

### 2. Install Dependencies

```bash
pip install langchain langchain-openai langchain-community faiss-cpu python-dotenv
```

---

### 3. Set Environment Variables

Create a `.env` file:

```env
OPENAI_API_KEY=your_api_key_here
```

---

## 🧩 Key Components Explained

### 🔹 1. Load Environment

```python
from dotenv import load_dotenv
import os

load_dotenv()
```

Loads API keys securely.

---

### 🔹 2. Load Data

```python
from langchain_community.document_loaders import TextLoader

loader = TextLoader("data.txt")
documents = loader.load()
```

Reads input text file.

---

### 🔹 3. Text Splitting

```python
from langchain.text_splitter import RecursiveCharacterTextSplitter

splitter = RecursiveCharacterTextSplitter(chunk_size=500, chunk_overlap=50)
docs = splitter.split_documents(documents)
```

Breaks large text into smaller chunks.

---

### 🔹 4. Embeddings

```python
from langchain_openai import OpenAIEmbeddings

embeddings = OpenAIEmbeddings()
```

Converts text into vectors for semantic search.

---

### 🔹 5. Vector Store (FAISS)

```python
from langchain_community.vectorstores import FAISS

vectorstore = FAISS.from_documents(docs, embeddings)
retriever = vectorstore.as_retriever()
```

Stores and retrieves relevant chunks.

---

### 🔹 6. Prompt Template

```python
from langchain_core.prompts import ChatPromptTemplate

prompt = ChatPromptTemplate.from_template(
    "Answer based only on the context:\n{context}\n\nQuestion: {question}"
)
```

Controls how LLM responds.

---

### 🔹 7. LLM Model

```python
from langchain_openai import ChatOpenAI

llm = ChatOpenAI(model="gpt-4o-mini")
```

Generates answers.

---

### 🔹 8. Chain Creation

```python
from langchain_core.runnables import RunnablePassthrough
from langchain_core.output_parsers import StrOutputParser

chain = (
    {
        "context": retriever,
        "question": RunnablePassthrough()
    }
    | prompt
    | llm
    | StrOutputParser()
)
```

Connects all components.

---

### 🔹 9. Run Query

```python
response = chain.invoke("What is this document about?")
print(response)
```

---

## 🧪 Example Use Case

* Question answering over documents
* Internal knowledge base
* Chat with your data

---

## 📌 Technologies Used

* LangChain
* OpenAI (LLM + Embeddings)
* FAISS (Vector Database)
* Python
* Google Colab

---

## ⚠️ Notes

* Ensure your OpenAI API key is valid
* FAISS runs locally (not for large-scale production)
* For production, consider Pinecone / Azure AI Search

---

## 🙌 Future Enhancements

* Add PDF/CSV loaders
* Use advanced vector DB (Pinecone)
* Deploy with FastAPI
* Add UI (Streamlit)

---

## 👨‍💻 Author

Saravanan

---

## ⭐ Support

If you like this project, give it a ⭐ on GitHub!
The folder which will have the work of RAG,LANGCHAIN,LANGGRAPH,AAGENTIC AI work
