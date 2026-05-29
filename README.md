# Finding Connections: GraphRAG Workshop

> **Neo4j Nodes 2025 Conference Workshop**

A hands-on workshop exploring GraphRAG — understanding not just *what* it is, but *why* it works and *how* each component contributes. The goal is to equip you with transferable skills and concepts you can remix for your own use cases.

## 🎯 Workshop Overview

GraphRAG combines **knowledge graphs** with **retrieval-augmented generation** to get better answers from language models. But GraphRAG is more than a single technique — it's an intersection of key technologies whose impact is still being discovered.

This workshop breaks down GraphRAG into its fundamental building blocks:

### Topics Covered

| Concept | What You'll Learn |
|---------|-------------------|
| **Graphs** | Nodes, edges, entities, and relationships |
| **RAG** | Retrieval Augmented Generation — putting relevant information into context |
| **Semantic Search** | Finding similar content through meaning, not just keywords |
| **Embeddings** | Converting text into numerical vectors that preserve semantic relationships |
| **Cosine Similarity** | Comparing vector directions in high-dimensional space |
| **Structured Data Extraction** | Getting structured output from unstructured text |
| **Constrained Decoding** | Guiding language models to produce schema-compliant responses |
| **GraphRAG Pipeline** | How all these pieces fit together end-to-end |

## 🚀 Getting Started

### Prerequisites

1. **Create a Neo4j account**: Visit [console.neo4j.io](https://console.neo4j.io/) and sign up
2. **Create a free instance**: Click "Create instance" in the Neo4j console
3. **Save your credentials**: Download the credentials file when prompted

### Using the LLM Graph Builder

1. Visit [llm-graph-builder.neo4jlabs.com](https://llm-graph-builder.neo4jlabs.com)
2. Click "Connect to Neo4j"
3. Upload your credentials file or enter connection details manually
4. Start exploring!

## 🔧 Key Technologies

### Embeddings

Text is converted into numerical vectors using specialized embedding models. These vectors capture semantic meaning — similar concepts end up with similar directions in vector space.

```python
from sentence_transformers import SentenceTransformer

model = SentenceTransformer("sentence-transformers/all-MiniLM-L6-v2")

# "The sun is shining" → 384-dimensional vector
embedding = model.encode("The sun is shining")
```

**Recommended model**: [all-MiniLM-L6-v2](https://huggingface.co/sentence-transformers/all-MiniLM-L6-v2) — lightweight, fast, and effective for semantic similarity.

### Structured Data Extraction

Language models can return structured data that fits a defined schema:

```python
from pydantic import BaseModel
from openai import OpenAI

class CalendarEvent(BaseModel):
    name: str
    date: str
    participants: list[str]

response = client.responses.parse(
    input=[
        {"role": "system", "content": "Extract the event information."},
        {"role": "user", "content": "Alice and Bob are going to a science fair on Friday."},
    ],
    text_format=CalendarEvent,
)
# → CalendarEvent(name='Science Fair', date='Friday', participants=['Alice', 'Bob'])
```

This uses **constrained decoding** — the model is restricted to only generating tokens that satisfy the schema.

### GraphRAG Pipeline

1. **Preprocessing**: Extract entities and relations from documents using structured data extraction
2. **Embedding**: Convert entities into vectors for semantic search
3. **Storage**: Add to a graph database (Neo4j)
4. **Querying**: Find similar entities via cosine similarity, traverse the graph for related information
5. **Generation**: Feed retrieved context to the language model alongside the question

## 📚 Resources

### GraphRAG Tools

| Tool | Description |
|------|-------------|
| [Microsoft GraphRAG](https://github.com/microsoft/graphrag) | Widely adopted, popular implementation |
| [GraphRAG Visualizer](https://github.com/noworneverev/graphrag-visualizer) | Visualize Microsoft GraphRAG outputs |
| [nano-graphrag](https://github.com/gusye1234/nano-graphrag) | Small, easy to hack on |
| [Neo4j GraphRAG Python](https://github.com/neo4j/neo4j-graphrag-python) | Neo4j ecosystem integration |
| [LLM Graph Builder](https://llm-graph-builder.neo4jlabs.com) | Interactive web tool for building graphs |

### Document Parsing

Language models work best with markdown. These tools help convert documents:

| Tool | Description |
|------|-------------|
| [Docling](https://github.com/docling-project/docling) | IBM Research — document understanding |
| [MarkItDown](https://github.com/microsoft/markitdown) | Microsoft — document to markdown conversion |

### Embedding Models

- [all-MiniLM-L6-v2](https://huggingface.co/sentence-transformers/all-MiniLM-L6-v2) — 384 dimensions, fast and lightweight
- [sentence-transformers](https://www.sbert.net/) — Framework for using and training embedding models

## 💡 Why This Matters

GraphRAG is a **gateway technology**. Each building block is valuable on its own:

- **Embeddings** power recommendation systems, anomaly detection, clustering, and more
- **Structured extraction** lets you build APIs over unstructured data
- **Graph databases** reveal hidden connections in any relational data
- **RAG** makes language models actually useful for domain-specific tasks

You don't need to adopt GraphRAG wholesale — understand the components, then remix them for your own problems.

## 👤 About the Presenter

**Johan** — [AI/Data engineering consultant](https://resolve.works) with over 15 years of building software, focused on ethical tech.

## 📂 Repository Contents

```
.
├── README.md          # This file
├── index.html         # Workshop presentation (Reveal.js)
├── CLAUDE.md          # Project context and guidelines
└── deepresearch.png   # Deep Research screenshot
```

## 📄 Slides

The presentation is built with [Reveal.js](https://revealjs.com/) and includes interactive visualizations:

- **Graph visualization** — D3.js force-directed graph showing entities and relationships
- **Vector space visualization** — 2D cosine similarity demonstration
- **Token probability charts** — How constrained decoding works
- **Dimension distance distributions** — Why cosine similarity beats Euclidean distance in high dimensions

To view the slides locally, simply open `index.html` in a browser.

---

*Workshop presented at [Neo4j Nodes 2025](https://neo4j.com/nodes/) — slides available at [nodes25.resolve.works](http://nodes25.resolve.works)*
