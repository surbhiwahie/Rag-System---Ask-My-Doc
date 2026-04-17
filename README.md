# Rag-System---Ask-My-Doc
Creating a RAG Systems - Healthcare Domain Specific - Ask My Doc


User Query
   ↓
answer_question()
   ↓
Retriever (Chroma)
   ↓
Top chunks
   ↓
Prompt + Context
   ↓
LLM (GPT)
   ↓
Final Answer + Citations

------ PHASE 2 -----------
Now we improve quality + accuracy + reliability

Step 1 — Hybrid Retrieval

Right now:
Vector Search ONLY

Problem:
Misses exact keywords sometimes
Struggles with precise terms
Solution: Hybrid Search

Combine:

Type	Strength
Semantic (current)	meaning
BM25 (keyword search)	exact match

For Example

Query:
"fasting plasma glucose threshold"

Vector → may miss exact phrase
BM25 → finds exact match

Combined = best result

What You’ll Add
BM25 retriever (keyword search)
Combine with your vector retriever

🥈 Step 2 — Reranking (BIG IMPACT)

Right now: Top K chunks (some noise): Add Cross-Encoder

Use models from:
Sentence Transformers

🧠 What It Does

Instead of: Query → embedding similarity

It does: Query + Chunk → scored together
(MUCH more accurate ranking)

🥉 Step 3 — Citation Enforcement (CRITICAL)

Right now:

LLM tries to cite
Upgrade it:

Force:

Each claim → must have source
Reject unsupported answers
🧪 Step 4 — Evaluation Framework (INTERVIEW GOLD)

Use:
👉 RAGAS

Build:
50–200 Q&A pairs
Manually verified
Measure:
Faithfulness
Answer correctness
Context relevance
🔥 This is HUGE

This step alone makes your project:

Recruiter-ready 🚀
🧰 Step 5 — Clean Project Structure (GitHub Ready)

Organize like:

rag-system/
│
├── data/
├── ingestion/
├── retrieval/
├── generation/
├── evaluation/
├── app/
├── .env.example
├── README.md
🎨 Step 6 (Optional but Powerful) — UI

Use:

Streamlit
Gradio

👉 Turn it into:

🎯 Goal

Combine them into ONE retriever

Hybrid Retriever = Vector + BM25
🧠 How It Works (Concept)

When user asks:

"What are symptoms of diabetes?"

We do:

Step 1: Vector → get top chunks
Step 2: BM25 → get top chunks
Step 3: Combine results
Step 4: Remove duplicates
----------
🧠 Final Clean Flow

Your notebook should look like:

✅ 1. Load + Chunk

✔️ already correct

✅ 2. Create Vector DB

✔️ already correct

✅ 3. Create Retrievers
vector_retriever
bm25_retriever
✅ 4. Hybrid Function
hybrid_retrieve()
✅ 5. LLM Setup
ChatOpenAI
✅ 6. Answer Function
answer_question()
✅ 7. Query
print(answer_question("your question"))
🧠 Mental Model Fix (VERY IMPORTANT)

Right now you had:

Vector Retriever → LLM

Now you have:

(Vector + BM25) → LLM

👉 This is a REAL upgrade

🧪 What You Should See Now

Try:

"What is blood sugar?"
"What are symptoms of diabetes?"
"What is insulin?"

👉 You should see:

better answers
more precise citations
fewer irrelevant chunks
🚀 You Just Completed
Phase 2 — Step 2: Hybrid Retrieval ✅


I’ve been working on building a domain-specific AI system called *“Ask My Doc.”* The goal is to create an intelligent assistant that can answer questions based strictly on internal documents like technical PDFs, healthcare documents, or contracts.

The key focus of this system is reliability and traceability. Instead of generating answers from general knowledge, it retrieves relevant information directly from the source documents and uses that as evidence to generate responses. Every answer includes citations, so users can clearly see where the information came from.

From a technical standpoint, the system works in a few stages:

First, I ingest documents such as PDFs and split them into smaller chunks to preserve context. These chunks are then converted into vector embeddings using a lightweight model—specifically *all-MiniLM-L6-v2* from the sentence-transformers family—which captures the semantic meaning of the text.

These embeddings are stored in a vector database—I'm currently using ChromaDB—which allows for efficient semantic search over the document corpus.

When a user asks a question, the system uses a hybrid retrieval approach. It combines semantic search from the vector database with keyword-based search using BM25. This helps balance understanding of meaning with exact term matching, which improves retrieval accuracy.

The retrieved chunks are then passed into a language model—I'm using *gpt-4o-mini*—which generates the final answer. The prompt is designed to be strict, so the model only answers based on the provided context and explicitly declines if the answer is not found, reducing hallucinations.

I’ve also implemented citation enforcement, so every response includes source references like document name and page number.

Currently, I’m working on improving the system further by adding a reranking layer using cross-encoder models to refine retrieval quality, and planning to build an evaluation pipeline to measure answer accuracy and faithfulness over time.

Overall, this project demonstrates how to build a reliable, explainable AI system that can work on domain-specific data while maintaining accuracy, transparency, and trust.
