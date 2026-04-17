
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
