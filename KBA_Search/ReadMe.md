# 📘 KBA Semantic Search System (Chunk-Based + Cosine Similarity)

An AI-powered Knowledge Base Article (KBA) search engine that uses **embeddings + FAISS vector database + cosine similarity** to retrieve the most relevant troubleshooting articles based on a new ticket description.

This project processes HTML-based KBA articles, converts them into embeddings, stores them in a vector database, and retrieves the best matching article using **chunk-level aggregation**.

---

## 🚀 Features

- ✅ Load multiple HTML KBA files from a folder  
- ✅ Extract clean text from HTML  
- ✅ Chunk large articles for better semantic accuracy  
- ✅ Generate embeddings using Ollama  
- ✅ Store vectors in FAISS  
- ✅ Use cosine similarity (`IndexFlatIP + L2 normalization`)  
- ✅ Retrieve top matching chunks  
- ✅ Aggregate chunk scores per article  
- ✅ Rank articles by combined similarity score  

---

## 🏗 Architecture
HTML KBA Files
↓
Text Extraction (BeautifulSoup)
↓
Chunking
↓
Embedding Generation (Ollama)
↓
Vector Storage (FAISS)
↓
Query Embedding
↓
Top-K Chunk Search
↓
Article Score Aggregation
↓
Best Matching KBA


---

## ⚙️ Installation

### 1️⃣ Clone Repository

```bash
git clone <your-repo-url>
cd kba-search
```
2️⃣ Install Dependencies
pip install faiss-cpu numpy beautifulsoup4 ollama
3️⃣ Install & Pull Embedding Model (Ollama)

Make sure Ollama is installed:
ollama pull nomic-embed-text

🧠 How It Works
1️⃣ Index KBA Articles
Reads all .html files from kba_articles/
Extracts clean text
Splits text into chunks
Creates embeddings
Normalizes vectors
Stores vectors in FAISS
Saves metadata mapping

2️⃣ Search for Similar KBA
Provide a new ticket description:
search_similar_kba("Root filesystem full causing SSH failure")

The system will:
Generate embedding for the ticket
Normalize vector
Search top 5 chunks
Group chunks by article
Sum similarity scores
Rank articles
Return best match

🔎 Cosine Similarity Implementation
faiss.IndexFlatIP(dimension)
faiss.normalize_L2(vector)

Why?
Inner Product (IP) becomes Cosine Similarity when vectors are normalized. This ensures semantic similarity based on vector direction, not magnitude.

📊 Example Output
🔍 Aggregated Article Ranking:

Article: OPS-1024
Total Combined Score: 1.72

Article: DB-204
Total Combined Score: 0.83

🏆 FINAL BEST MATCH
Article: OPS-1024
🧩 Metadata Structure

Each stored chunk has metadata:

[
  {
    "article_name": "OPS-1024",
    "source_file": "OPS-1024.html",
    "chunk_id": 0
  }
]

This ensures proper mapping between:
FAISS Index Position → Chunk → Article

🧠 Tech Stack
-Python
-FAISS
-Ollama (Embeddings)
-BeautifulSoup
-NumPy

🎯 Use Cases
-IT ticket auto-resolution
-Enterprise knowledge retrieval
-Internal documentation search
-DevOps troubleshooting assistant
-Support automation system

🛡 Production Recommendations
-Always normalize vectors before storing & searching
-Keep FAISS and metadata order synchronized
-Chunk large documents (800–1000 characters recommended)
-Validate embedding dimensions before search

