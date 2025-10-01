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
- Uses **Llama 3 (via Ollama + LangChain)** to break your text into `(head → relation → tail)` triples.  
- Example:  
  - `thunderstorm → occurs over → lighthouse`  
  - `thunderstorm → produces → thunder sound`  

### 📊 Knowledge Graph Visualization  
- Triples are converted into a **knowledge graph** using `networkx`.  
- Visualized with `matplotlib` for transparency and explainability.  

### 🎨 Image Generation  
- **Stable Diffusion (sd-turbo)** generates images based on the **entities and relations** in the graph.  
- Ensures visual output is **faithful to the structure** of the text.  

### 🔊 Audio Generation  
- **MusicGen (facebook/musicgen-small)** generates **sound effects or short audio clips**.  
- Example: For “thunderstorm,” it produces **thunder sounds** to complement the generated image.  

---

## 🏛️ Architecture  

1. **Input Module** → Accepts natural language prompts  
2. **Reasoning Module** → Llama 3 + LangChain extract triples  
3. **Knowledge Graph Module** → Builds/visualizes a graph  
4. **Decision Module** → Chooses image and/or audio generation  
5. **Image Generation Module** → Stable Diffusion produces visuals  
6. **Audio Generation Module** → MusicGen produces sounds  
7. **Output Module** → Packages results: graph PNG, generated image, audio file  

---

## 🔄 Data Flow  

1. **User Prompt** →  
   *“Show me a dramatic thunderstorm over a lighthouse and also provide how thunder sounds.”*  
2. **Triple Extraction** →  
   - `thunderstorm → occurs over → lighthouse`  
   - `thunderstorm → produces → thunder sound`  
3. **Knowledge Graph** → nodes = entities, edges = relations  
4. **Decision Logic** → detects visual & sound cues  
5. **Generation** →  
   - Image → Stable Diffusion  
   - Audio → MusicGen  
6. **Outputs** →  
   - Graph (`kg_graph.png`)  
   - Image (`generated.png`)  
   - Audio (`generated.wav`)  

---

## ⚠️ Limitations  

- **Performance:** CPU inference works but is slow. GPU recommended (Colab/Kaggle free GPU).  
- **Memory Usage:** Stable Diffusion may crash on GPUs < 6 GB VRAM unless reduced resolution/steps are used.  
- **Audio Length:** MusicGen outputs are short clips (~10 seconds).  
- **Extraction Accuracy:** Llama 3 triple extraction may misinterpret complex sentences.  
- **Generative Fidelity:** Generated image/audio may not always perfectly match input prompt.  
- **Infra Dependency:** Ollama is required locally for Llama 3; Colab setup is smoother.  

---

## ⚡ Quickstart  

### Run Locally
```bash
git clone https://github.com/yourusername/multimodal-ai-poc.git
cd multimodal-ai-poc
pip install -r requirements.txt
