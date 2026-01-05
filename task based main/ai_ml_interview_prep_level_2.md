---
> **✨ Created by Thiyagarajan Varadharajan ✨**  
> *Python Full Stack Developer | Interview Prep Resources*

---

# AI/ML & LLM Mastery - Level 2 (Dual Approach)

This guide focuses on **Method 1 (Manual/Scratch Logic)** vs **Method 2 (Modern Framework/API)** for advanced AI implementation.

---

## **Section 1: Transformers & LLMs (Q26-38)**

### **26. Attention Mechanism**
**Task:** Explain and implement the core concept of weighting word importance.

#### **Method 1: Manual Dot-Product (Scratch)**
```python
import numpy as np
# Logic: Query x Key = Weight. Weight x Value = Attention Result.
Q = np.array([1, 0])
K = np.array([1, 0])
V = np.array([10, 20])
score = np.dot(Q, K) # Result: 1 (High match)
output = score * V # Focus on the first element
```

#### **Method 2: MultiHeadAttention (PyTorch/DL)**
```python
import torch.nn as nn
# Logic: High-level layer that handles multiple 'heads' of attention simultaneously.
attention = nn.MultiheadAttention(embed_dim=128, num_heads=8)
```

---

### **27. Retrieval Augmented Generation (RAG)**
**Task:** How to give an LLM private knowledge.

#### **Method 1: Manual RAG (Python + Index)**
```python
# Logic: 
# 1. Search text file for keywords. 
# 2. Append matched lines to the prompt manually.
prompt = f"Context: {found_lines}\nQuestion: {query}"
```

#### **Method 2: LangChain RAG (Modern Pipeline)**
```python
from langchain.chains import RetrievalQA
# Logic: Automated orchestration of Embeddings -> VectorDB -> Prompt -> LLM.
chain = RetrievalQA.from_chain_type(llm=openai, retriever=vectordb.as_retriever())
```

---

### **28. Vector Search**
**Task:** Find the most similar sentences.

#### **Method 1: Cosine Similarity (Stat)**
```python
from sklearn.metrics.pairwise import cosine_similarity
# Logic: Mathematical calculation of the angle between two vectors.
# 1.0 = Perfect match, 0.0 = No relation.
score = cosine_similarity(vec1, vec2)
```

#### **Method 2: Vector DB (ChromaDB)**
```python
collection.query(query_embeddings=[vec1], n_results=2)
# Logic: Uses HNSW or similar algorithms for lightning-fast search on millions of vectors.
```

---

### **29. Model Deployment**
**Task:** How to run an LLM for your users.

#### **Method 1: Local Hosting (Llama-CPP)**
```python
from llama_cpp import Llama
# Logic: Runs GGUF quantized models on your own CPU/GPU locally.
llm = Llama(model_path="llama-2-7b.gguf")
```

#### **Method 2: API Hosting (OpenAI/Azure)**
```python
import openai
# Logic: Managed service. No infrastructure management, pay-per-token.
response = openai.ChatCompletion.create(model="gpt-4", messages=[...])
```

---

### **30. Prompt Engineering**
**Task:** Guiding the model to act as a specific persona.

#### **Method 1: Single-Line instruction**
```text
"Solve this math problem: 2+2"
```

#### **Method 2: System Prompting (Modern)**
```python
# Logic: Setting a 'Mental State' for the model separate from the user query.
messages = [
    {"role": "system", "content": "You are a helpful math teacher who explains steps."},
    {"role": "user", "content": "2+2"}
]
```

---

## **Section 2: RAG Micro-Project (Q36-45)**

### **36. Full RAG Logic Comparison**

| Phase | Approach A (Manual Scratch) | Approach B (LangChain/Framework) |
|---|---|---|
| **Chunking** | String slice by `\n\n` | RecursiveCharacterTextSplitter |
| **Embeddings** | TF-IDF (Stat) | HuggingFaceEmbeddings (DL) |
| **Search** | Loop through every line | Index-based (FAISS/Chroma) |
| **LLM Inference**| `requests.post` to API | `llm_chain.run()` |

---

### **37. Handling Large Context**
**Task:** What to do when the PDF is bigger than the "Context Window".

#### **Method 1: Truncation (Chop)**
```python
# Logic: Simply only send the first 2000 words to the LLM.
context = pdf_text[:2000]
```

#### **Method 2: Map-Reduce (Modern)**
```python
# Logic: 1. Summarize chunks separately. 2. Summarize the summaries.
# This preserves the general meaning of the whole document.
```

---

### **40. Error Handling (Hallucinations)**
**Task:** Stop the AI from lying.

#### **Approach 1: Self-Correct Loop**
```python
# Logic: Ask AI "Is this answer grounded in the context?". If "No", regenerate.
```

#### **Approach 2: Verification Chains (RAGAS / Evaluation)**
```python
# Logic: Use a second 'Guardian' model to verify the primary model's output.
```


---

> **✨ Created by Thiyagarajan Varadharajan ✨**  
> *Python Full Stack Developer | Interview Prep Resources*
> 
> *Share this resource on LinkedIn!*

---
