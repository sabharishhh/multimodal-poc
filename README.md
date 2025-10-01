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
- Extracts **structured knowledge** from text using **Llama 3 + LangChain**.  
- Converts natural language into `(head → relation → tail)` triples.  
- Example:  
  - `thunderstorm → occurs over → lighthouse`  
  - `thunderstorm → produces → thunder sound`  

### 📊 Knowledge Graph Visualization  
- Builds a **knowledge graph** with `networkx`.  
- Visualizes it using `matplotlib`.  
- Provides **explainability** — you can see exactly what the AI understood before generation.  

### 🎨 Image Generation  
- Detects visual cues in the graph.  
- Generates images using **Stable Diffusion (sd-turbo)**.  
- Ensures generated visuals are **faithful to the structured description**.  

### 🔊 Audio Generation  
- Detects sound-related cues in the graph.  
- Uses **MusicGen (facebook/musicgen-small)** to generate **environmental sounds or music**.  
- Example: A thunderstorm produces both a **visual storm scene** and the **sound of thunder**.  

---

## 🏛️ Architecture  

The pipeline is modular, with each stage handling a distinct task:  

1. **Input Module** – Accepts natural language user prompts.  
2. **Reasoning Module** – Extracts triples via Llama 3 + LangChain.  
3. **Knowledge Graph Module** – Builds and visualizes the graph.  
4. **Decision Module** – Decides between image and/or audio generation.  
5. **Image Generation Module** – Stable Diffusion creates visuals.  
6. **Audio Generation Module** – MusicGen generates sounds.  
7. **Output Module** – Packages graph, image, and audio into results.  

---

## 🔄 Data Flow  

The system processes information step by step:  

1. **User Prompt** – e.g.  
   *“Show me a dramatic thunderstorm over a lighthouse and also provide how thunder sounds.”*  

2. **Entity & Relation Extraction** – Extract triples:  
   - `thunderstorm → occurs over → lighthouse`  
   - `thunderstorm → produces → thunder sound`  

3. **Knowledge Graph Construction** – Build and visualize graph with entities + relations.  

4. **Modality Decision** – Detect if image or audio generation is needed.  

5. **Image Generation** – Stable Diffusion renders a storm scene over a lighthouse.  

6. **Audio Generation** – MusicGen produces a thunder sound clip.  

7. **Final Output** – You get:  
   - Knowledge graph visualization.  
   - Generated image.  
   - Generated audio.  

---

## 🖼 Example  

**Prompt:**  
```text
Show me a dramatic thunderstorm over a lighthouse and also provide how thunder sounds.
