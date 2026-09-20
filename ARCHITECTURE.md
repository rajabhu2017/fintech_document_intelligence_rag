# Architecture

## High-Level

```text
                    INGESTION
┌─────────────┐
│  PDF Upload │
└──────┬──────┘
       ↓
┌───────────────────┐
│ Default Data      │
│ Loader            │
└──────┬────────────┘
       ↓
┌───────────────────┐
│ Recursive          │
│ Character Splitter │
└──────┬────────────┘
       ↓
┌───────────────────┐
│ Gemini Embeddings │
│ gemini-embedding-001
└──────┬────────────┘
       ↓
┌──────────────────────────────┐
│ Pinecone                     │
│ Vector + Metadata            │
│                              │
│ document_id                  │
│ document_name                │
│ document_type                │
│ version                      │
│ source                       │
│ upload_date                  │
└──────────────┬───────────────┘
               ↑
               │
               │ semantic retrieval
               │
┌──────────────┴───────────────┐
│       fintech_document_search│
└──────────────┬───────────────┘
               ↑
               │
        ┌──────┴──────┐
        │  AI Agent   │
        └──────┬──────┘
               ↑
        ┌──────┴──────┐
        │User Question│
        └─────────────┘
               ↓
       Grounded Response
       + Source Evidence
```

## Design Principles

- Ingestion and retrieval are separate concerns.
- The same embedding model/configuration is used for document vectors and query vectors.
- Persistent vector storage separates knowledge from temporary workflow state.
- Metadata provides provenance and future filtering capability.
- The agent is instructed to retrieve before answering.
- Unsupported questions should produce a not-found response rather than an unsupported answer.
