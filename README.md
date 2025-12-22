# 🔍 Retrieval-Augmented Generation (RAG) Project

This project implements a **three-layer RAG architecture** to build an effective and explainable search system over a Kaggle dataset. The layers include:

1. **Embedding Layer**  
2. **Search Layer**  
3. **Generation Layer**

---

## 📘 1️⃣ Embedding Layer

This layer is responsible for preprocessing the PDF, chunking the content, and embedding it into a vector space for semantic search.

### ✅ Steps:
- **Chunk** the content: (skipped for this project)
  - Fixed-size chunks 
  - Sentence-based or paragraph-based chunking
- **Embed** the chunks using:
  - `OpenAIEmbedding` model *(via OpenAI API)*
  - Or any model from **SentenceTransformers** (e.g., `all-MiniLM-L6-v2`, `multi-qa-MiniLM`, etc.)
- **Store** the embeddings in a **ChromaDB** vector database for fast retrieval.

---

##  2️⃣ Search Layer

This layer handles the semantic search using user queries and reranks the results for improved relevance.

### ✅ Steps:
- Design at least **3 queries** based on the document 
- **Embed** the queries using the same embedding model.
- **Search ChromaDB** to retrieve top-N relevant chunks.
- Implement a **caching mechanism** to avoid reprocessing repeated queries.
- Apply a **Cross-Encoder Re-ranker** (e.g. `cross-encoder/ms-marco-MiniLM-L-6-v2`) from HuggingFace to re-score and reorder the retrieved chunks.

---

##  3️⃣ Generation Layer

This layer generates the final answer by feeding the top reranked chunks into a powerful LLM.

### ✅ Steps:
- Construct a **detailed prompt** that includes:
  - The user query
  - The top-3 reranked chunks as context
  - Clear instructions on how to answer
- Use **OpenAI GPT-4**, **GPT-3.5**, or any open-source instruction-tuned LLM to generate the final response. I have used Open source Huggingface model
- Optionally include **few-shot examples** to improve generation quality.

###  Required Outputs:
- **Final answer generated** by the LLM  for each query

---

## ✅ Summary :
- 📄 Chunked and embedded document (stored in ChromaDB)
- 🔍 Query → Top-N results → Re-ranked results
- 🧾 Prompt → Answer from LLM

Query:  Any floral palazzo pants in size M, preferably under ₹1500?

top results
1. Libas Women Pink Floral Printed Ethnic Palazzos - This product is available in size M and is priced at ₹1,499.
2. Indo Era Women Brown Solid Straight Palazzos - This product is available in size M and is priced at ₹1,499.
3. W Yellow Palazzos - This product is available in size M and is priced at ₹1,499.

 <img width="1425" height="593" alt="image" src="https://github.com/user-attachments/assets/47ebf1dc-2d24-45e4-852e-74623b51cdb7" />


---
