# Multimodal AI POC  

This repository contains a **proof-of-concept multimodal AI pipeline** that combines **knowledge graph extraction, text-to-image, and text-to-audio generation** into a single workflow.  

The goal is to demonstrate how **structured reasoning (via knowledge graphs)** can guide **generative AI models** to produce more meaningful and consistent multimodal outputs.  

---

## ✨ Features
- **Entity & Relation Extraction**  
  - Uses **Llama 3 (via Ollama + LangChain)** to extract `(head, relation, tail)` triples from natural language.  
- **Knowledge Graph Visualization**  
  - Builds graphs with `networkx` and visualizes them using `matplotlib`.  
- **Image Generation**  
  - Employs **Stable Diffusion (sd-turbo)** to generate images guided by graph entities and relations.  
- **Audio Generation**  
  - Leverages **MusicGen (facebook/musicgen-small)** to create environmental sounds or musical snippets.  

---

## 🖼 Example

**Prompt:**  
```text
Show me a dramatic thunderstorm over a lighthouse and also provide how thunder sounds.
