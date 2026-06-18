<div align="center">

# ✍️ WriteRight

### *AI Handwriting Feedback*

Write or draw a letter on the canvas and get instant, AI-powered feedback on your handwriting - scored across six areas, with tips and practice exercises to improve.

![Python](https://img.shields.io/badge/Python-3.10+-blue?logo=python&logoColor=white)
![Flask](https://img.shields.io/badge/Flask-000000?logo=flask&logoColor=white)
![Gemini](https://img.shields.io/badge/Google_Gemini-Multimodal-4285F4?logo=google&logoColor=white)
![Render](https://img.shields.io/badge/Backend-Render-46E3B7)
![Netlify](https://img.shields.io/badge/Frontend-Netlify-00C7B7?logo=netlify&logoColor=white)

[**🌐 Live Demo**](https://fanciful-cheesecake-a69e49.netlify.app/)

</div>

---

## ✨ Overview

**WriteRight** is a handwriting-practice web app. Instead of uploading a photo, you write or draw directly on a canvas using a mouse, touchscreen, or stylus. The drawing is sent to **Google's Gemini multimodal model**, which reads the text, evaluates the handwriting, and returns structured feedback with numeric scores and practice steps.

---

## 🌸 Features

-  **Draw-to-analyze canvas** - write with a mouse, touchscreen, or stylus; no photo or upload needed
-  **Gemini multimodal AI** reads the handwriting and assesses it
-  **Six scoring areas** - legibility, letter formation, spacing, baseline consistency, size consistency, and slant consistency
-  **Actionable feedback** - strengths, areas to improve, tips, and step-by-step practice exercises
-  **Model fallback chain** - automatically tries multiple Gemini versions so the app keeps working if one is unavailable
-  **Live deployment** - Flask API on Render, frontend on Netlify

---

## 🧩 Tech Stack

| Layer        | Technology                                  |
| ------------ | ------------------------------------------- |
|  Frontend  | HTML, CSS, JavaScript (canvas), Netlify     |
|  Backend   | Python, Flask, gunicorn, Render             |
|  AI Model  | Google Gemini (multimodal)                  |
|  Imaging   | Pillow (PIL)                                |

---

## 🏗️ How It Works
1. The user draws on a canvas in the browser; the drawing is captured as an image.
2. The frontend sends it to the Flask backend's `/analyze` endpoint.
3. Gemini reads the text and rates the handwriting; the backend parses the model's reply into a clean JSON structure (scores, strengths, improvements, tips, practice steps).
4. The frontend displays the scores and feedback.

A key part of the backend is a **parsing layer** that turns Gemini's free-form text reply into a strict JSON schema, with regex fallbacks for when the output isn't clean - so the frontend always receives predictable, structured data.

```
Canvas (Draw Handwriting)
          │
          ▼
Capture as Image
          │
          ▼
POST Request
          │
          ▼
Flask Backend (Render)
          │
          ▼
Google Gemini Multimodal API
          │
          ▼
AI evaluates handwriting
          │
          ▼
JSON Response
          │
          ▼
Display Score & Feedback
```

## 📂 Project Structure

```text
WriteRight/
│
├── backend/
│   ├── backend.py          # Flask backend application
│   ├── requirements.txt    # Python dependencies
│   ├── runtime.txt         # Python runtime version for deployment
│   ├── render.yaml         # Render deployment configuration
│   ├── .gitignore          # Git ignored files
│   └── venv/               # Virtual environment (not committed)
│
├── frontend/
│   └── index.html          # Frontend interface with drawing canvas
│
└── README.md               # Project documentation
```

## 🚀 Run Locally

### Backend

```bash
cd backend
pip install -r requirements.txt
```

Create a `.env` file in `backend/` with your Gemini API key:
> 🔑 Get a key at [Google AI Studio](https://aistudio.google.com/app/apikey).

Then run:

```bash
python app.py
```

The API starts at `http://localhost:5000`.

### Frontend

Open `frontend/index.html` in your browser. Make sure its API URL points at your backend (`http://localhost:5000` for local, or your Render URL when deployed).

---

## 🔌 API

| Method | Route          | Description                                              |
| ------ | -------------- | ------------------------------------------------------- |
| `GET`  | `/health`      | Health check                                            |
| `POST` | `/detect-text` | Returns the text recognized in the handwriting image    |
| `POST` | `/analyze`     | Returns full analysis: scores, strengths, tips, steps   |

---

## 🔐 Security Notes

-  The Gemini API key is read from an environment variable, never hardcoded
-  `.env` is excluded from version control via `.gitignore`
-  **Never commit secrets or API keys to the repository**

---

## 🌱 Future Improvements

- Save progress over time to track improvement
- Support long sentences
- Compare attempts side-by-side
- Mobile application

---
