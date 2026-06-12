<div align="center">

# 📚 BookBuddy

### *Your AI-powered reading companion — ask anything, discover everything.*

[![Python](https://img.shields.io/badge/Python-3.10+-3776AB?style=for-the-badge&logo=python&logoColor=white)](https://python.org)
[![Streamlit](https://img.shields.io/badge/Streamlit-FF4B4B?style=for-the-badge&logo=streamlit&logoColor=white)](https://streamlit.io)
[![LangChain](https://img.shields.io/badge/LangChain-1C3C3C?style=for-the-badge&logo=langchain&logoColor=white)](https://langchain.com)
[![MistralAI](https://img.shields.io/badge/Mistral_AI-FF7000?style=for-the-badge&logo=mistral&logoColor=white)](https://mistral.ai)
[![ChromaDB](https://img.shields.io/badge/ChromaDB-orange?style=for-the-badge)](https://www.trychroma.com)

<br/>

> 📖 Upload a PDF. Ask a question. Get answers — directly from the book.

</div>

---

## ✨ What is BookBuddy?

**BookBuddy** is a local RAG (Retrieval-Augmented Generation) application that lets you have a conversation with any PDF document. Whether it's a textbook, research paper, novel, or technical manual — just upload it and start asking questions.

No more ctrl+F. No more skimming. Just ask.

---

## 🚀 Features

- 📄 **PDF Upload & Processing** — Drop any PDF and BookBuddy will chunk and embed it automatically
- 🧠 **Semantic Search** — Uses HuggingFace embeddings to find the most relevant passages, not just keywords
- 🔍 **MMR Retrieval** — Maximal Marginal Relevance ensures diverse, non-redundant context is fetched
- 💬 **Mistral-Powered Answers** — Uses `mistral-small-2506` to generate grounded, context-aware responses
- 🗃️ **Persistent Vector Store** — ChromaDB persists your embeddings so you don't reprocess on every run
- 🖥️ **Two Interfaces** — A polished Streamlit web UI *and* a fast terminal-based chat interface

---

## 🛠️ Tech Stack

| Layer | Technology |
|---|---|
| 🧩 Framework | LangChain |
| 🤖 LLM | Mistral AI (`mistral-small-2506`) |
| 🔢 Embeddings | HuggingFace Sentence Transformers |
| 🗄️ Vector DB | ChromaDB |
| 📑 PDF Loader | PyPDFLoader |
| 🖥️ UI | Streamlit |

---

## 📁 Project Structure

```
BookBuddy/
│
├── app.py                # 🌐 Streamlit web app (upload PDF + chat UI)
├── main.py               # 💻 Terminal-based RAG chat interface
├── create_database.py    # 🗃️ Standalone script to build the vector DB
├── requirements.txt      # 📦 All dependencies
└── .env                  # 🔑 API keys (not committed)
```

---

## ⚙️ Setup & Installation

### 1. Clone the repository

```bash
git clone https://github.com/ramya-rastogi/BookBuddy.git
cd BookBuddy
```

### 2. Create a virtual environment

```bash
python -m venv venv
source venv/bin/activate        # On Windows: venv\Scripts\activate
```

### 3. Install dependencies

```bash
pip install -r requirements.txt
```

### 4. Set up your environment variables

Create a `.env` file in the project root:

```env
MISTRAL_API_KEY=your_mistral_api_key_here
```

> 💡 Get your Mistral API key at [console.mistral.ai](https://console.mistral.ai)

---

## 🎮 Usage

### 🌐 Option A — Streamlit Web App (Recommended)

```bash
streamlit run app.py
```

Then open your browser at `http://localhost:8501`.

**Steps:**
1. Upload a PDF using the file uploader
2. Click **"Create Vector Database"** to embed and index the document
3. Type your question in the input box and get an AI-generated answer

---

### 💻 Option B — Terminal Chat Interface

**Step 1:** Build the vector database (edit the PDF path in `create_database.py` first)

```bash
python create_database.py
```

**Step 2:** Start chatting

```bash
python main.py
```

```
Rag system created
press 0 to exit
You : What is backpropagation?

AI: Backpropagation is an algorithm used to train neural networks by...
```

Type `0` to exit the session.

---

## 🧠 How It Works

```
[ Your PDF ]
     │
     ▼
[ PyPDFLoader ] ──► Loads all pages as Documents
     │
     ▼
[ Text Splitter ] ──► Chunks into 1000-char pieces (200 overlap)
     │
     ▼
[ HuggingFace Embeddings ] ──► Converts chunks to vectors
     │
     ▼
[ ChromaDB ] ──► Stores & persists all vectors locally
     │
     ▼
[ Your Question ]
     │
     ▼
[ MMR Retriever ] ──► Fetches top 4 relevant + diverse chunks
     │
     ▼
[ Mistral AI ] ──► Generates answer using only retrieved context
     │
     ▼
[ You get your answer ✅ ]
```

---

## 🔧 Configuration

You can tune the RAG behavior by modifying these parameters:

| Parameter | Location | Default | Effect |
|---|---|---|---|
| `chunk_size` | `app.py`, `create_database.py` | `1000` | Larger = more context per chunk |
| `chunk_overlap` | `app.py`, `create_database.py` | `200` | Higher = less info lost at boundaries |
| `k` | `app.py`, `main.py` | `4` | Number of chunks retrieved |
| `fetch_k` | `app.py`, `main.py` | `10` | Pool size for MMR selection |
| `lambda_mult` | `app.py`, `main.py` | `0.5` | 0 = max diversity, 1 = max relevance |

---






*Stop searching. Start asking.*

</div>
