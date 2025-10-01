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

## 🔄 How Data Flows  

This project follows a **step-by-step multimodal pipeline**, where text is first understood, then structured, and finally transformed into visuals and sounds.  

1. **User Prompt**  
   - You provide a natural language input, e.g.:  
     *“Show me a dramatic thunderstorm over a lighthouse and also provide how thunder sounds.”*  

2. **Entity & Relation Extraction**  
   - The text is passed to **Llama 3 via LangChain**.  
   - The model extracts `(head, relation, tail)` triples like:  
     - `thunderstorm → occurs over → lighthouse`  
     - `thunderstorm → produces → thunder sound`  

3. **Knowledge Graph Construction**  
   - Triples are turned into a **graph** with `networkx`.  
   - Nodes = entities (e.g., thunderstorm, lighthouse).  
   - Edges = relationships (e.g., produces, occurs over).  
   - This graph is also visualized so you can see what the system “understood”.  

4. **Modality Decision**  
   - Based on the graph:  
     - If there are **visual entities/relations**, trigger **image generation**.  
     - If there are **sound-related entities/relations**, trigger **audio generation**.  

5. **Image Generation**  
   - **Stable Diffusion (sd-turbo)** creates an image using structured graph prompts.  
   - Example: A stormy sky above a lighthouse on a rugged coast.  

6. **Audio Generation**  
   - **MusicGen** generates an audio snippet matching the sound cues.  
   - Example: A short thunderclap recording.  

7. **Final Output**  
   - The system produces a package of results:  
     - **Knowledge Graph image** (what was understood).  
     - **Generated Image** (visual scene).  
     - **Generated Audio** (environmental sound).  

📦 **End result:** You get a synchronized experience of structured reasoning (graph) + visual imagination (image) + audio ambience (sound).  


---

## 🖼 Example

**Prompt:**  
```text
Show me a dramatic thunderstorm over a lighthouse and also provide how thunder sounds.
