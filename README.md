🧠 DontForget: Neural Database Engine
DontForget is a local neural database implemented with FastAPI, SQLite, OpenAI embeddings, and a Text-to-SQL helper. It follows the hybrid architecture from Neural Databases Using Large Language Models: SPO triplet storage, keyword search, vector search, gated knowledge edits, and LLM-based reranking/synthesis.

Features
SPO triplet storage for structured memory retrieval.
Hybrid retrieval that combines SQLite FTS5 keyword search with OpenAI embedding similarity.
Knowledge editing with the gating rule gate = σ(sim(q,k)/τ) to override stale facts.
Natural language to SQL translation against an external SQLite database.
LLM reranking for better result ordering before synthesis.
Setup
Requirements
Python 3.10+
OPENAI_API_KEY
DONTFORGET_SECRET_KEY
Install dependencies on Windows
python -m venv .venv
.\.venv\Scripts\Activate.ps1
python -m pip install --upgrade pip
python -m pip install fastapi uvicorn python-dotenv openai pydantic numpy
Configure environment variables
Create a .env file in the project root with:

OPENAI_API_KEY=sk-...
DONTFORGET_SECRET_KEY=your_secret
Run the app
python main.py
If the environment is configured correctly, FastAPI starts with Uvicorn on http://0.0.0.0:8001.

Verified run (Windows venv):

.\.venv\Scripts\Activate.ps1
\.venv\Scripts\python.exe main.py
When started successfully the server listens on http://0.0.0.0:8001.

Use the CLI helper
mem is a Bash script, so run it from Git Bash, WSL, or another POSIX shell:

export DONTFORGET_API_URL="http://0.0.0.0:8001"
export DONTFORGET_SECRET_KEY="your_secret"
bash mem q "How much do I owe Akash?"
Usage
Remember a thought
mem r "Paid 432 rs to Akash for dinner"
Query memory
mem q "How much do I owe Akash?"
Delete matching memories
mem d "That note about Akash"
Edit a fact
mem e "How much I owe Akash" "I paid Akash back, debt is cleared"
Ask Text-to-SQL questions
mem sql "How many users signed up last month?" "/path/to/app.db"
Architecture
Ingestion: text → tags + SPO triplets + embedding → SQLite storage.
Retrieval: query → keyword extraction → hybrid search → knowledge edits → reranking → synthesis.
T2SQL: question → schema extraction → few-shot prompting → SQL generation → execution.
Editing: edited facts are stored separately and override matching retrievals when the gate passes.
API Endpoints
Endpoint	Method	Description
/remember	POST	Store a memory with tags, triplets, and an embedding
/remind	POST	Query memories using hybrid search and synthesis
/delete	POST	Delete memories by natural language description
/edit	POST	Store a knowledge edit
/t2sql	POST	Translate natural language to SQL and run it on a SQLite DB
Research Paper
Neural database using large language model
