# 🌐 Multimodal AI POC  

![Python](https://img.shields.io/badge/python-3.10%2B-blue.svg)  
![License](https://img.shields.io/badge/license-MIT-green.svg)  
![HuggingFace](https://img.shields.io/badge/models-HuggingFace-orange.svg)  
[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/)

This repository contains a **proof-of-concept multimodal AI pipeline** that combines **knowledge graph extraction, text-to-image, and text-to-audio generation** into a single workflow.  

The goal is to demonstrate how **structured reasoning (via knowledge graphs)** can guide **generative AI models** to produce more meaningful and consistent multimodal outputs.  

---

## ✨ Features  

### 🧠 Entity & Relation Extraction  
The pipeline doesn’t just read your input like plain text—it **understands the structure**.  
Using **Llama 3 with LangChain**, it breaks your description into `(head → relation → tail)` triples.  

For example:  
- `thunderstorm → occurs over → lighthouse`  
- `thunderstorm → produces → thunder sound`  

This structured representation helps the rest of the system know *what objects exist* and *how they are connected*.  

---

### 📊 Knowledge Graph Visualization  
The extracted triples are turned into a **knowledge graph** using `networkx` and visualized with `matplotlib`.  
Each entity becomes a node, and each relation is drawn as a labeled edge.  

This makes the pipeline **explainable**—you can actually see what the AI understood before it generates images or sounds.  

---

### 🎨 Image Generation  
With the knowledge graph in hand, the system knows which parts of your text should be treated as **visual elements** (like “thunderstorm” or “lighthouse”).  
These cues are passed into **Stable Diffusion (sd-turbo)**, which generates an image that reflects both the entities *and* their relationships.  

This ensures the image isn’t just random—it stays **faithful to the structure of your description**.  

---

### 🔊 Audio Generation  
If the graph indicates anything sound-related (like “thunder”, “waves crashing”, or “birds singing”), the system activates **MusicGen (facebook/musicgen-small)**.  

It produces **environmental audio snippets or sound effects** that bring the scene to life.  
For example: if your input says *“thunderstorm”*, you’ll get not just the picture of the storm, but also the **sound of thunder** to go with it.  


---

## 🖼 Example

**Prompt:**  
```text
Show me a dramatic thunderstorm over a lighthouse and also provide how thunder sounds.
