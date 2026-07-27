# Simple RAG System

A lightweight retrieval-augmented generation pipeline that answers questions grounded in a small set of documents, using FAISS for retrieval and a local LLM for generation.


- **Vector DB:** FAISS
- **Embedding model:** all-MiniLM-L6-v2 (sentence-transformers)
- **LLM:** qwen2.5:3b via local Ollama API
- **Docs:** 10 short ML/AI concept files, chunked by paragraph (~120 words/chunk)
- **Grounding rule:** prompt instructs the model to answer only from retrieved context, or say it cannot answer

## Example Q&A

All correctly-scoped questions (LoRA, gradient descent, precision/recall, self-attention) were answered correctly, grounded in the retrieved document chunks.

**Q: What is the capital of France? (out of scope)**
A: "I cannot answer this based on the provided documents."
**Why:** FAISS always returns its top-k nearest chunks, even if none are truly relevant. The LLM correctly noticed the retrieved context didn't answer the question and refused, instead of falling back on its own general knowledge.

## Files
- Notebook (RAG pipeline)
- `docs/` - 10 source documents (ML/AI concepts)

## Run
Make sure Ollama is running with `qwen2.5:3b` pulled, then run the notebook top to bottom. Use `generate_answer("your question")` to query.
