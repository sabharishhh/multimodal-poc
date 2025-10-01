# 🌐 Multimodal AI POC  

![Python](https://img.shields.io/badge/python-3.10%2B-blue.svg)  
![License](https://img.shields.io/badge/license-MIT-green.svg)  
![HuggingFace](https://img.shields.io/badge/models-HuggingFace-orange.svg)  
[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/)

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
