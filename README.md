# Multi-Agent Regulatory Assistant

## RAG

Key considerations for the RAG implementation

- **Content extraction**:
  - **Done**: Extract text from PDF documents using `pymupdf` library.
    - *Pros*: Easy to use. Provide 'good' content extraction.
    - *Cons*: /. (Might not be the best out there?)
  - **To Do**: Reformat extracted text to filter out irrelevant content (e.g. headers, page numbers, whitespaces/newlines).
- **Document chunking**: 
  - **Done**: Chunk documents into manageable subparts using pages. Add source and page number metadata to allow easy frontend display of source documents.
    - *Pros*: Easy to implement.
    - *Cons*: May separate related information across different pages.
  - **To Do**: Summarize or compress pages to reduce token count. Chunk documents into relevant sections/subsections (instead of using full pages).
- **Document embedding**:
  - **Done**: Embed documents based using ChromaDB (using default parameters).
    - *Pros*: Easy to implement, customizable.
    - *Cons*: /.
  - **To Do**: Use more advanced LLM embedder. Create persistent DB provider on a server (instead of local). Remove collected telemetry (is it really stopped?). Multi-modal support.
- **Document retrieval**: Fetch relevant documents based on a query.
  - **Done**: Embed query (using same embedder as docs) and fetch `n` relevant documents (using default parameters).
    - *Pros*: Easy to implement, customizable.
    - *Cons*: /.
  - **To Do**: Put threshold distance instead of fecthing `n` docs (based on dataset). Structure output format to allow frontend display of source documents.

## Prompting Structure

**General Structure**: Impersonation and short description as system instructions.
- **Agent**: Tool calling based on query and context (memory)
  - **Done**: Reasoning prompt structure, examples of tool calling (for few-shot inference), tools explanations and structured output via tools definition.
    - **Pros**: Use structured output with tool handling (using MCP standard). Almost complete structure allowing good alignement of orchestrator.
    - **Cons**: Model not really reasoning.
  - **To Do**: Should structure output even more with clear reasoning/planning as output next to function calling (to allow real reasoning/planning). Memory/context selection/compression/isolation (see https://rlancemartin.github.io/2025/06/23/context_engineering/).
- **Response Tool**: Simple tool to output final response of agent (mandatory, so automatically added to all agents as a tool).
  - **Done**: Simple prompt/tool to reformat output. Added automatically to all agents.
    - **Pros**: Simple and efficient.
    - **Cons**: Prompt engineering missing to tailor output. 
  - **To Do**: Prompt engineering to align outputs to the desired style. Play with max output tokens to reduce cost?

## Agent Orchestration

Structure:

```bash
Agent [Orchestrator]
├── Agent [RAG]
|   ├── Tool [Vector DB]
|   └── Tool [Response Tool]
└── Tool [Response Tool]
```
  
**Agent**: Tool calling based on query and context (memory)
  - **Done**: Reasoning prompt structure, examples of tool calling (for few-shot inference), tools explanations, and structured output via tools definition.
    - **Pros**: Use structured output with tool handling (using MCP standard). Almost complete structure allowing good alignement of orchestrator.
    - **Cons**: Model not really reasoning.
  - **To Do**: Should structure output even more with clear reasoning/planning as output next to function calling (to allow real reasoning/planning). Memory/context selection/compression/isolation (see https://rlancemartin.github.io/2025/06/23/context_engineering/).