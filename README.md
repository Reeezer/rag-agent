# Custom Agent Framework for RAG

<a name="top"></a>

## Table of Contents

- [About](#-about)
- [Documentation](#-documentation)
- [Getting Started](#-getting-started)

## 🚀 About

This project is the **base for a hand-made framework** to build retrieval-augmented assistants.  
It’s designed as a modular foundation: documents are ingested, searched, and reasoned over by **agents** that orchestrate specialized **tools**. The structure makes it easy to extend with new retrieval methods, models, or task-specific logic.

⚡ This is just the starting point: the codebase doubles as a lightweight, hand-crafted framework for building custom agentic workflows around documents and retrieval.

## 📚 Documentation 

### What It Does

1. **Ingests documents**  
   - Scans a `data/` folder for PDFs.  
   - Extracts page-level text using `PyMuPDF`.  
   - Creates a searchable collection with **ChromaDB**.  

2. **Retrieves relevant content**  
   - Queries the vector store with natural-language questions.  
   - Surfaces the most relevant document passages, with metadata (source and page number).  

3. **Generates responses**  
   - Uses **Google Gemini** models to reason over retrieved passages.  
   - Produces concise, context-grounded answers.  

4. **Coordinates reasoning with agents**  
   - An **Orchestrator agent** decides how to break down a query.  
   - Specialized **tools** (retrieval, response generation, etc.) handle subtasks.  
   - Agents maintain a short-term **memory** of queries and tool outputs, enabling iterative refinement.  

### Tech Stack

- **Document parsing**: [PyMuPDF](https://pymupdf.readthedocs.io/en/latest/)
- **Vector DB**: [ChromaDB](https://www.trychroma.com/)
- **LLM API**: [Google Gemini](https://ai.google.dev/)
- **Configuration**: `.env` for API keys
- **Framework**: Agent + Tool abstraction using Pydantic models

## 📝 Getting Started

```bash
python main.py
```

Example Query:

```bash
Compare FDA and WHO approaches to risk management for medical devices
```

Example Flow:

1. Orchestrator agent receives the query.
2. Delegates retrieval to the RAG tool.
3. Retrieves relevant pages from FDA and WHO docs.
4. Passes results to the Response tool.
5. Outputs a concise, well-grounded comparison.



[Back to top](#top)
