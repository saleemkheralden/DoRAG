# DoRAG (DockerRAG)

## Overview
DoRAG is an open-source document ingestion and retrieval system that transforms unstructured documents into structured, searchable knowledge and retrieval-ready indexes.

It is designed as an infrastructure layer for building RAG applications on top of large document collections.

## Problem

Modern RAG systems are usually:

- hard to configure
- inconsistent across projects
- dependent on manual preprocessing
- tightly coupled to specific frameworks

Users repeatedly rebuild the same pipeline:

- document parsing
- chunking strategies
- embedding generation
- vector indexing
- metadata handling

DoRAG aims to standardize and automate this pipeline.

## Core Idea

> Turn unstructured documents into structured knowledge automatically.

DoRAG handles the entire ingestion lifecycle:

### Processing pipeline


1. Document 
2. Type Detection 
3. Metadata Extraction 
4. Smart Chunking 
5. Concept/Knowledge Extraction 
6. Indexing 
7. Retrieval-Ready Storage


### Storage (parallel flow)

| Step id	| Step					| Storage				|
| --------- | --------------------- | ---------------------	|
| 1			| Document				| Raw Storage			|
| 2			| Type Detection		| Metadata stored in DB	|
| 3			| Metadata Extraction 	| DB					|
| 4			| Smart Chunking		| Chunk table in DB		|
| 5			| Concept Extraction	| Concept table in DB	|
| 6			| Indexing				| Vector DB				|



## Key Features (MVP)

### 1. Automatic Document Ingestion

Supports:

- PDFs
- Markdown
- Plain text (initially)

### 2. Document Type Detection

Automatically identifies:

- research papers
- books
- technical documentation
- generic text

### 3. Metadata Extraction

Extracts:

- title
- authors (if applicable)
- structure (sections, headers)
- document type

### 4. Smart Chunking

Multiple strategies depending on document type:

- section-based chunking (papers)
- header-based chunking (markdown)
- paragraph-based fallback

### 5. Concept Extraction (lightweight MVP version)

Extracts:

- key concepts
- keywords
- topics

(No graph or relationships yet)

### 6. Indexing Layer

Stores:

- structured metadata (DB)
- embeddings (vector DB)

### 7. Retrieval API

Provides:

- semantic search
- metadata filtering
- retrieval-ready context for LLMs

## Architecture


```
                ┌──────────────┐
                │  Documents   │
                └──────┬───────┘
                       ▼
            ┌─────────────────────┐
            │  Ingestion Layer    │
            │ - type detection    │
            │ - metadata extract  │
            └──────────┬──────────┘
                       ▼
            ┌─────────────────────┐
            │  Chunking Engine    │
            │ - smart strategies  │
            └──────────┬──────────┘
                       ▼
            ┌─────────────────────┐
            │ Concept Extraction  │
            └──────────┬──────────┘
                       ▼
        ┌────────────────────────────┐
        │ Storage Layer              │
        │ - DB                       │
        │ - Vector Database          │
        └─────────────┬──────────────┘
                      ▼
             ┌─────────────────┐
             │ Retrieval API   │
             └─────────────────┘
```

## What DoRAG is NOT
- Not a chatbot
- Not a full AI agent system
- Not a knowledge graph system (yet)
- Not a research discovery engine
- Not a UI-first product

It is **infrastructure** for RAG systems.

## Roadmap
### Phase 1 — Core ingestion system

- document upload
- parsing
- chunking
- embedding
- storage
- retrieval API

### Phase 2 — Smart processing

- improved chunking strategies
- better metadata extraction
- concept extraction improvements

### Future (not committed)
- knowledge graph builder
- recommendation system
- research exploration layer
- multi-document reasoning engine

### Design Principles
- Automation over configuration
- Deterministic pipelines
- Reproducibility
- Storage-first architecture
- Extensible processing stages

## License

Apache License 2.0

## Why this exists

DoRAG exists because building a reliable RAG pipeline from scratch should not require reimplementing ingestion, chunking, embedding, and indexing logic every time.


