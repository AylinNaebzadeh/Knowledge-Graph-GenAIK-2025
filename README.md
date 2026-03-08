# 🌌 Exploiting Geoffrey Hinton's Knowledge Graph
## Overview

## Knowledge Graph Construction
### Data Collection and Filtering
I began by collecting all relevant Wikipedia pages that encompass various aspects of Hinton’s work. This dataset included key contributions, collaborations, and inventions. To refine the knowledge graph and ensure its focus on the most impactful elements of Hinton’s work, I filtered the documents to highlight:
- Individuals with close collaborations with Hinton.
- Key inventions and research milestones associated with his contributions.
### Data Segmentation
To manage the large volume of content, I segmented the documents into smaller, manageable chunks while preserving contextual continuity. Using the **Mistral 7B** model and a `MapReduce` chain, I performed a two-phase summarization:
1. Initial Extraction: Identified the key information in each document chunk.
2. Consolidation: Combined the extracted information to generate one single summary of the main themes.
### Entity and Relationship Extraction
To extract important entities and relationships from the summary, I employed a few-shot prompt engineering technique. This method allowed me to define an output format that included: 
- `Head`: The main entity in the relationship.
- `Head_Type`: The type of entity (e.g., `person`, 
`institution`).
- `Tail`: The entity linked to the head.
- `Tail_Type`: The type of the related entity (e.g., `invention`, `award`). 
I used the **Llama3-70b-8192 model**, accessed via the **Groq API**, with the `temperature` set to zero to ensure non-creative responses. The extracted entities and relations focused on pre-defined categories such as person, institution, award, and invention, and relations such as `coAuthored`, `worksAt`, and `hasAward`.
## HybridRAG Development
  ### TODO
 ## Knowledge Graph Embeddings Evaluation
  ### TODO
## 📝 Sources:
- https://github.com/mallahyari/twosetai/blob/main/02_kg_construction.ipynb
- https://github.com/projectwilsen/KnowledgeGraphLLM 
