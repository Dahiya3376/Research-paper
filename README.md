# 🧠 DontForget: Neural Database Engine

DontForget is a local hybrid neural database engine built using **FastAPI**, **SQLite**, **OpenAI Embeddings**, and **Large Language Models (LLMs)**. It enables intelligent memory storage, semantic retrieval, natural language querying, and Text-to-SQL generation through a lightweight and scalable architecture.

The project follows the research concepts presented in **“Neural Databases Using Large Language Models”**, combining structured memory retrieval with neural semantic search for efficient and user-friendly database interaction.

---

# 🚀 Features

* **SPO Triplet Storage**
  Stores memories in Subject–Predicate–Object format for structured semantic retrieval.

* **Hybrid Retrieval System**
  Combines:

  * SQLite FTS5 keyword search
  * OpenAI embedding similarity search

* **Knowledge Editing with Gating**
  Uses the gating function:

  ```math
  gate = σ(sim(q,k)/τ)
  ```

  to override stale facts with updated information.

* **Natural Language to SQL (Text-to-SQL)**
  Converts plain English questions into executable SQL queries for external SQLite databases.

* **LLM-Based Reranking & Synthesis**
  Uses LLMs to rerank retrieved memories and generate coherent responses.

* **FastAPI Backend**
  Lightweight REST API with Uvicorn support.

* **Local-First Architecture**
  Runs fully on local infrastructure using SQLite storage.

---

# 🏗️ Architecture

## 1. Ingestion Pipeline

```text
Text Input
   ↓
Tag Extraction
   ↓
SPO Triplet Generation
   ↓
Embedding Creation
   ↓
SQLite Storage
```

---

## 2. Retrieval Pipeline

```text
User Query
   ↓
Keyword Extraction
   ↓
Hybrid Search
   ├── FTS5 Keyword Search
   └── Vector Similarity Search
   ↓
Knowledge Edit Override
   ↓
LLM Reranking
   ↓
Answer Synthesis
```

---

## 3. Text-to-SQL Pipeline

```text
Natural Language Question
   ↓
Schema Extraction
   ↓
Few-Shot Prompting
   ↓
SQL Generation
   ↓
SQLite Execution
```

---

# ⚙️ Tech Stack

| Technology        | Purpose                     |
| ----------------- | --------------------------- |
| FastAPI           | Backend API                 |
| SQLite + FTS5     | Storage & keyword retrieval |
| OpenAI Embeddings | Semantic vector search      |
| Python            | Core backend logic          |
| NumPy             | Vector operations           |
| Uvicorn           | ASGI server                 |
| Pydantic          | Data validation             |
| LLMs              | Reranking & synthesis       |

---

# 📦 Installation

## Requirements

* Python 3.10+
* OpenAI API Key
* Secret Key

---

## Clone Repository

```bash
git clone https://github.com/yourusername/dontforget.git
cd dontforget
```

---

# 🪟 Windows Setup

## Create Virtual Environment

```powershell
python -m venv .venv
```

## Activate Environment

```powershell
.\.venv\Scripts\Activate.ps1
```

## Install Dependencies

```powershell
python -m pip install --upgrade pip
python -m pip install fastapi uvicorn python-dotenv openai pydantic numpy
```

---

# 🔑 Environment Variables

Create a `.env` file in the project root:

```env
OPENAI_API_KEY=sk-xxxxxxxxxxxxxxxx
DONTFORGET_SECRET_KEY=your_secret_key
```

---

# ▶️ Run the Server

```bash
python main.py
```

If configured correctly, FastAPI starts with Uvicorn on:

```text
http://0.0.0.0:8001
```

---

# ✅ Verified Windows Run

```powershell
.\.venv\Scripts\Activate.ps1
.\.venv\Scripts\python.exe main.py
```

---

# 💻 CLI Helper Usage

The `mem` helper script works in:

* Git Bash
* WSL
* Linux/macOS terminals

---

## Configure CLI

```bash
export DONTFORGET_API_URL="http://0.0.0.0:8001"
export DONTFORGET_SECRET_KEY="your_secret_key"
```

---

# 🧠 Memory Commands

## Remember a Thought

```bash
bash mem r "Paid 432 rs to Akash for dinner"
```

---

## Query Memory

```bash
bash mem q "How much do I owe Akash?"
```

---

## Delete Memories

```bash
bash mem d "That note about Akash"
```

---

## Edit Existing Knowledge

```bash
bash mem e "How much I owe Akash" "I paid Akash back, debt is cleared"
```

---

## Ask SQL Questions

```bash
bash mem sql "How many users signed up last month?" "/path/to/app.db"
```

---

# 📡 API Endpoints

| Endpoint    | Method | Description                                 |
| ----------- | ------ | ------------------------------------------- |
| `/remember` | POST   | Store memories with embeddings and triplets |
| `/remind`   | POST   | Query memory using hybrid retrieval         |
| `/delete`   | POST   | Delete memories using natural language      |
| `/edit`     | POST   | Store knowledge edits                       |
| `/t2sql`    | POST   | Generate and execute SQL queries            |

---

# 🧪 Example Workflow

## Store Memory

```bash
bash mem r "Rahul borrowed 500 rs from me"
```

## Query Memory

```bash
bash mem q "Who borrowed money from me?"
```

## Edit Memory

```bash
bash mem e "Rahul borrowed 500 rs" "Rahul repaid the money"
```

---

# 🔬 Research Inspiration

This project is based on the concepts discussed in:

## **Neural Databases Using Large Language Models**

Key ideas implemented:

* Hybrid neural retrieval
* SPO memory representation
* Semantic vector search
* Text-to-SQL translation
* Knowledge editing and override gating
* LLM reranking and synthesis

---

# 📈 Future Improvements

* PostgreSQL + pgvector support
* HNSW vector indexing
* Multi-user authentication
* LangChain integration
* Streaming responses
* Multilingual querying
* Graph-based memory reasoning
* Docker deployment

---

# 🤝 Contributing

Contributions are welcome.

1. Fork the repository
2. Create a feature branch
3. Commit changes
4. Open a pull request

---

# 📄 License

This project is licensed under the MIT License.

---

# 👨‍💻 Author

**Mukul Dahiya**
Computer Science Engineering
Chitkara University

---

# ⭐ Support

If you like this project, consider giving it a ⭐ on GitHub.
