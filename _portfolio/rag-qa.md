---
title: "RAG Q&A System"
excerpt: "Production-ready Retrieval-Augmented Generation system with Docling for high-fidelity document parsing and hybrid retrieval."
header:
  teaser: /assets/portfolio/RAG_QA/img1.png
collection: portfolio
order: 7
tech: ["Docling", "LangChain", "FAISS", "GPT-4", "Python"]
github_url: "https://github.com/tuandoan998/Practical-RAG"
---

A production-grade RAG system built on the principle that retrieval quality is the primary bottleneck in most RAG deployments. The system uses Docling for high-fidelity parsing, hybrid retrieval (keyword + semantic), and re-ranking — the components that matter most in practice.

## Gallery

![RAG system architecture](/assets/portfolio/RAG_QA/img1.png)

![RAG evaluation dashboard](/assets/portfolio/RAG_QA/img2.png)

## Architecture

```
Documents (PDF, DOCX, XLSX, PPTX)
        ↓
   Docling Parser (layout-aware chunking)
        ↓
   Hybrid Index (BM25 + Dense Embeddings)
        ↓
   Retrieval → Re-ranking (cross-encoder)
        ↓
   GPT-4 Generation with citations
        ↓
   RAGAs / DeepEval evaluation
```

## Key Features

- **Docling parsing**: Preserves table structure, headings, and reading order across complex PDFs
- **Hybrid retrieval**: BM25 for exact keyword match + dense embeddings for semantic similarity
- **Re-ranking**: Cross-encoder scores top-k candidates for precision
- **Evaluation**: Automated RAGAs metrics (faithfulness, relevancy, context precision) on every change
- **Multi-format**: Handles PDF, DOCX, XLSX, and PPTX in a unified pipeline
