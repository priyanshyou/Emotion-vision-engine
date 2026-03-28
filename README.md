# 🎙️ The Empathy Engine — Giving AI a Human Voice

A service that **dynamically modulates Text-to-Speech (TTS) vocal characteristics** based on detected text emotion. It bridges the gap between text-based sentiment and expressive, human-like audio output.

## ✨ Features

- **5 Granular Emotion Categories**: Excited, Happy, Neutral, Sad, Angry
- **3 Vocal Parameters Modulated**: Speech Rate, Volume, Pitch
- **Intensity Scaling**: Stronger emotions produce larger vocal deviations
- **Real-time Sentiment Analysis**: Powered by VADER (Valence Aware Dictionary and sEntiment Reasoner)
- **Offline TTS**: No API keys required — runs fully locally with pyttsx3
- **Premium Web UI**: Dark-themed glassmorphism interface with live emotion visualization
- **RESTful API**: Clean JSON API for programmatic access
<img width="1900" height="1075" alt="image" src="https://github.com/user-attachments/assets/d6cc7dfc-9815-465b-b63f-2851c69fea3d" />
<img width="1903" height="1072" alt="image" src="https://github.com/user-attachments/assets/b826a4f1-6422-4166-b3c8-8c2217683cf4" />
<img width="1882" height="1078" alt="image" src="https://github.com/user-attachments/assets/0ddf13c7-6783-4a9d-8bfc-0120fdad6766" />



## 🏗️ Architecture

```
Text Input → Emotion Detection (VADER) → Voice Mapping → TTS Synthesis (pyttsx3) → Audio Output (.wav)
```

### Emotion-to-Voice Mapping Logic

| Emotion  | Speech Rate    | Volume         | Pitch          | Description                     |
|----------|---------------|----------------|----------------|---------------------------------|
| Excited  | Fast (220 wpm)| Loud (1.0)     | High           | Energetic, enthusiastic         |
| Happy    | Mod-fast      | Mod-loud       | Medium-High    | Warm, upbeat                    |
| Neutral  | Normal (160)  | Normal (0.75)  | Normal         | Balanced, clear                 |
| Sad      | Slow (120)    | Soft (0.55)    | Low            | Somber, reflective              |
| Angry    | Fast (200)    | Loud (1.0)     | Low-Forceful   | Intense, sharp                  |

**Intensity Scaling**: Parameters are interpolated between neutral baseline and emotion target based on the emotion's intensity score (0.0–1.0). For example, "I'm okay" (mildly happy) produces a slight rate increase, while "This is the BEST DAY EVER!" produces a much larger increase.

## 🚀 Quick Start

### Prerequisites
- Python 3.9+
- Windows (pyttsx3 uses SAPI5 on Windows)

### Installation

```bash
# Clone the repository
git clone <https://github.com/priyanshyou/Emotion-vision-engine.git>
cd Priyanshu_Darwix

# Install dependencies
pip install -r requirements.txt
```

### Run the Application

```bash
python -m uvicorn app.main:app --host 0.0.0.0 --port 8000 --reload
```

Then open **http://localhost:8000** in your browser.

## 📡 API Endpoints

### `POST /api/analyze`
Analyze text emotion without generating audio.

```json
// Request
{ "text": "This is amazing news!" }

// Response
{
  "emotion": {
    "label": "Excited",
    "intensity": 0.802,
    "confidence": 0.736,
    "compound": 0.8016,
    "scores": { "positive": 0.368, "negative": 0.0, "neutral": 0.632 },
    "description": "Strongly positive — enthusiastic, thrilled, overjoyed"
  },
  "voice_config": {
    "rate": 208,
    "volume": 0.95,
    "pitch_label": "High",
    "description": "Fast, loud, high-pitched — energetic and enthusiastic"
  }
}
```

### `POST /api/synthesize`
Full pipeline: detect emotion → map voice → generate TTS audio.

```json
// Request
{ "text": "I'm so disappointed with this result." }

// Response
{
  "emotion": { ... },
  "voice_config": { ... },
  "audio_url": "/audio/empathy_abc123.wav",
  "success": true
}
```

### `GET /api/voices`
List available system TTS voices.

### `GET /api/health`
Health check endpoint.

## 🛠️ Tech Stack

| Component            | Technology       |
|---------------------|-----------------|
| Language            | Python 3.9+     |
| Web Framework       | FastAPI          |
| Sentiment Analysis  | VADER Sentiment  |
| Text-to-Speech      | pyttsx3 (SAPI5)  |
| Frontend            | Vanilla HTML/CSS/JS |

## 📁 Project Structure

```
Priyanshu_Darwix/
├── app/
│   ├── __init__.py
│   ├── main.py              # FastAPI application & routes
│   ├── emotion_detector.py  # VADER-based emotion analysis
│   ├── voice_mapper.py      # Emotion → voice parameter mapping
│   └── tts_engine.py        # pyttsx3 TTS with thread-safe worker
├── static/
│   ├── index.html           # Web UI
│   ├── style.css            # Premium dark theme
│   └── app.js               # Frontend logic
├── audio_output/            # Generated .wav files
├── requirements.txt
└── README.md
```

## 📄 License

Built for the Darwix AI Hackathon Challenge 1.
