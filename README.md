# 🎙️🖼️ The Empathy Vision Engine

A comprehensive service that combines **Emotion-Driven Neural Voice Synthesis** with **Automated Narrative Storyboarding**. It bridges the gap between text-based sentiment, expressive human-like audio output, and cohesive visual storytelling. 

Built for the **Darwix AI Hackathon Challenges 1 & 2**.

## ✨ Features

### 🗣️ Challenge 1: Neural Voice & Emotion Detection
- **5 Granular Emotion Categories**: Excited, Happy, Neutral, Sad, Angry
- **3 Vocal Parameters Modulated**: Speech Rate, Volume, Pitch
- **Intensity Scaling**: Stronger emotions produce larger vocal deviations
- **Real-time Sentiment Analysis**: Powered by VADER (Valence Aware Dictionary and sEntiment Reasoner)
- **Offline TTS**: No API keys required — runs fully locally with pyttsx3

### 🎨 Challenge 2: Automated Storyboard Generation
- **Intelligent Narrative Segmentation**: Uses NLTK to seamlessly chunk continuous text into logical scenes.
- **Rule-Based Prompt Engineering**: Context-aware prompt generation to ensure high-quality images.
- **5 Preset Aesthetic Styles**: Photorealistic, Digital Art, Cyberpunk, Watercolor, and Minimalist Vector.
- **Dynamic Image Generation**: Real-time visualization via external image APIs (`api.airforce/v1/imagine2`).

### 💻 System & UI
- **Premium Web UI**: Dark-themed glassmorphism interface with live emotion parsing and storyboard rendering.
- **RESTful API**: Clean JSON API for programmatic access to both audio and visual pipelines.

### Image
<img width="1900" height="1075" alt="image" src="https://github.com/user-attachments/assets/d6cc7dfc-9815-465b-b63f-2851c69fea3d" />
<img width="1903" height="1072" alt="image" src="https://github.com/user-attachments/assets/b826a4f1-6422-4166-b3c8-8c2217683cf4" />
<img width="1882" height="1078" alt="image" src="https://github.com/user-attachments/assets/0ddf13c7-6783-4a9d-8bfc-0120fdad6766" />

## 🏗️ Architecture

```
Text Input 👇
 ├─> Emotion Detection (VADER) ─> Voice Mapping ─> TTS Synthesis (pyttsx3) ─> 🎵 Audio Output
 └─> Scene Segmentation (NLTK) ─> Prompt Engineering ─> External Image Generation ─> 🖼️ Storyboard Panels
```

### Emotion-to-Voice Logic
Parameters are interpolated between a neutral baseline and expected target based on emotion intensity (0.0-1.0).

## 🚀 Quick Start

### Prerequisites
- Python 3.9+
- Windows (pyttsx3 uses SAPI5 on Windows natively)

### Installation

```bash
# Clone the repository
git clone <https://github.com/priyanshyou/Emotion-vision-engine.git>
cd Priyanshu_Darwix

# Install dependencies (NLTK data will auto-download on first run)
pip install -r requirements.txt
```

### Run the Application

```bash
python -m uvicorn app.main:app --host 0.0.0.0 --port 8000 --reload
```

Then open **http://localhost:8000** in your browser.

## 📡 API Endpoints

### Voice Engine
- `POST /api/analyze`: Analyze text emotion without generating audio.
- `POST /api/synthesize`: Detect emotion → map voice → generate TTS audio.
- `GET /api/voices`: List available system TTS voices.

### Storyboard Engine
- *(Endpoints defined in `main.py` handle passing text through the `storyboard_engine` to return image arrays)*.

### System
- `GET /api/health`: Health check endpoint.

## 🛠️ Tech Stack

| Component            | Technology       |
|---------------------|-----------------|
| Backend Language    | Python 3.9+     |
| Web Framework       | FastAPI          |
| Sentiment Analysis  | VADER Sentiment  |
| Text-to-Speech      | pyttsx3 (SAPI5)  |
| NLP Segmentation    | NLTK (punkt)   |
| Front-end & UI      | Vanilla HTML/CSS/JS |
