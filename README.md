# 🌌 Exploiting Geoffrey Hinton's Knowledge Graph

## Overview
This project focuses on constructing a knowledge graph centered on **Geoffrey Hinton’s contributions to artificial intelligence** and leveraging it within a **Hybrid Retrieval-Augmented Generation (Hybrid RAG)** system.  

The goal is to combine **structured knowledge graph retrieval** with **unstructured text retrieval** to improve the quality and accuracy of generated responses about Geoffrey Hinton's work, collaborations, and achievements.

---

# Knowledge Graph Construction

## Data Collection and Filtering
I began by collecting relevant Wikipedia pages covering different aspects of **Geoffrey Hinton’s work**, including his collaborations, research contributions, and major inventions.

To ensure the knowledge graph focuses on the most impactful elements of Hinton’s career, I filtered the collected documents to highlight:

- Individuals who closely collaborated with Hinton  
- Key inventions and research milestones related to his work  

---

## Data Segmentation
Because the collected documents were large, I segmented them into smaller, manageable chunks while preserving contextual continuity.

Using the **Mistral 7B** model and a `MapReduce` chain, I performed a two-phase summarization process:

1. **Initial Extraction**  
   Key information was identified within each document chunk.

2. **Consolidation**  
   The extracted information from all chunks was combined to generate a single summary capturing the main themes.

---

## Entity and Relationship Extraction
To extract important entities and relationships from the summary, I applied a **few-shot prompt engineering** technique. This approach allowed me to enforce a structured output format containing the following fields:

- **Head** — The main entity in the relationship  
- **Head_Type** — The type of the entity (e.g., `person`, `institution`)  
- **Tail** — The entity connected to the head  
- **Tail_Type** — The type of the related entity (e.g., `invention`, `award`)  

For extraction, I used the **Llama3-70b-8192 model** accessed through the **Groq API**, with the `temperature` parameter set to `0` to ensure deterministic responses.

The extracted entities and relationships were restricted to predefined categories such as:

**Entity Types**
- `person`
- `institution`
- `award`
- `invention`

**Relation Types**
- `coAuthored`
- `worksAt`
- `hasAward`

---

# Hybrid RAG Development

## Retrieval Process
The retrieval pipeline begins when a user submits a question.

The query is passed to a **RAG retriever** that searches across both:

- **Unstructured text data**, using keyword and vector-based search  
- **Structured knowledge graph data**, using graph-based retrieval  

For vector search, embeddings from the **all-MiniLM-L12** model are used.

---

## Graph-Based Retrieval
The graph retriever identifies key entities in the user query using an LLM.

Once relevant entities are detected, I use a **full-text index** to map them to nodes in the knowledge graph. The process involves:

### Entity Detection
The LLM identifies important entities within the user query.

### Full-Text Indexing
The detected entities are mapped to the knowledge graph using a **full-text index**, which allows tolerance for minor spelling variations.

---

## RAG Chain Completion
After retrieval is completed, a **final prompt** is generated using the retrieved context.

This prompt is passed to a generative model that produces the final response. The Hybrid RAG system therefore combines:

- **Knowledge graph reasoning**
- **Vector retrieval**
- **Generative language modeling**

For the final generation step, I use the **Llama3-70b-8192** model to produce answers based on the retrieved information.

## 📝 Sources:
- https://github.com/mallahyari/twosetai/blob/main/02_kg_construction.ipynb
- https://github.com/projectwilsen/KnowledgeGraphLLM 
