---
title: "Car Retrieval System"
excerpt: "Metric learning pipeline for car identification and retrieval using deep learning embeddings and cosine similarity search."
header:
  teaser: /assets/portfolio/car_retrieval/car_retrieval.png
collection: portfolio
order: 1
tech: ["DeiT", "Metric Learning", "TripletMargin Loss", "Cosine Similarity", "PyTorch"]
blog_url: "https://tuandoan998.github.io/posts/2026/04/carnet/"
---

A machine learning pipeline for car identification and retrieval using deep learning embeddings. The system trains a metric learning model to produce discriminative embeddings, then retrieves visually similar cars from a reference gallery via exact cosine similarity search.

## Gallery

![Car retrieval overview](/assets/portfolio/car_retrieval/car_retrieval.png)

![Retrieval result 1](/assets/portfolio/car_retrieval/car_retrieval_1.png)

![Retrieval result 2](/assets/portfolio/car_retrieval/car_retrieval_2.png)

![Demo GIF](/assets/portfolio/car_retrieval/car_retrieval.gif)

## Key Features

- **Embedding model**: Fine-tuned DeiT (Data-efficient Image Transformer) with TripletMargin loss for discriminative metric learning
- **Gallery search**: Exact cosine similarity against a pre-built reference gallery
- **Scalable**: Embeddings can be indexed with FAISS for large-scale retrieval
- **End-to-end**: Single image in → ranked list of matching cars out

## Architecture

```
Input Image → DeiT Backbone → L2-normalized Embedding
                                      ↓
                             Cosine Similarity Search
                                      ↓
                             Ranked Gallery Results
```
