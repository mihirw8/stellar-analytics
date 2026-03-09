# 🌌 Stellar Analytics
### Exoplanet Signal Classifier & Radius Predictor
**TECHNEX '26 · IIT BHU · Innorave Eco-Hackathon**

[![Backend](https://img.shields.io/badge/Backend-Live-4ade80?style=flat-square&logo=render)](https://stellar-analytics-backend.onrender.com/)
[![Frontend](https://img.shields.io/badge/Frontend-Live-60a5fa?style=flat-square&logo=render)](https://static-stellar-analytics.onrender.com/)
[![Python](https://img.shields.io/badge/Python-3.11-yellow?style=flat-square&logo=python)](https://python.org)
[![React](https://img.shields.io/badge/React-18-61dafb?style=flat-square&logo=react)](https://react.dev)

---

## 🏆 Final Scores

| Task | Metric | Score |
|------|--------|-------|
| A — Classification | F1-Score | **0.9200** |
| A — Classification | ROC-AUC | **0.9848** |
| B — Regression | RMSE | **0.4838** |
| B — Regression | MAE | **0.1533** |

---

## 🚀 Live Demo

> ⚠️ **IMPORTANT — Read this before opening the app**
>
> The backend is hosted on **Render Free Tier** which spins down after 15 minutes of inactivity.
> You MUST wake up the backend before using the frontend, otherwise you will get API errors.

### Step 1 — Wake up the Backend (do this first!)

Open this URL in your browser and wait until you see a JSON response:

```
https://stellar-analytics-backend.onrender.com/health
```

You should see:
```json
{
  "status": "ok",
  "models_loaded": true,
  "features_A": 18,
  "features_B": 11
}
```

⏳ **This may take 30–60 seconds** on first load — Render is waking up the server. Wait until you see the JSON before proceeding.

### Step 2 — Open the Frontend

Once the backend is awake, open the frontend:

```
https://static-stellar-analytics.onrender.com/
```

The app should now work fully with no API errors.

---

## 🎯 Project Overview

The Stellar Analytics challenge tasks participants with building an end-to-end ML system to analyze **Kepler Objects of Interest (KOIs)** from NASA's Kepler Space Telescope mission.

| Task | Description | Model | Key Metric |
|------|-------------|-------|-----------|
| **Task A** | Classify signals as CONFIRMED planet or FALSE POSITIVE | XGBoost | F1: 0.9200 |
| **Task B** | Predict planetary radius in Earth radii | LightGBM | RMSE: 0.4838 |

---

## ✨ Features

- 🔭 **Single Prediction** — Enter KOI parameters and get instant classification + radius prediction
- 📂 **Batch CSV Upload** — Upload hundreds of rows at once, download results as CSV
- 📊 **Data Insights** — EDA visualizations, feature correlations, importance charts
- 🔄 **Pipeline View** — Interactive step-by-step ML pipeline diagram
- 📖 **About** — Full methodology, model comparison, team info
- 📋 **History** — Last 20 predictions with timestamps

---

## 🛠️ Tech Stack

| Layer | Technology |
|-------|-----------|
| ML Models | XGBoost, LightGBM, Scikit-learn 1.8.0 |
| Backend | Python 3.11, Flask, Flask-CORS, Gunicorn |
| Frontend | React 18, Vite |
| Deployment | Render (backend + frontend) |
| Data | NASA Kepler KOI Dataset (7,585 records) |



## 🔌 API Endpoints

| Method | Endpoint | Description |
|--------|----------|-------------|
| GET | `/health` | Health check + model status |
| POST | `/predict/full` | Run Task A + Task B together |
| POST | `/predict/classify` | Task A classification only |
| POST | `/predict/radius` | Task B regression only |
| GET | `/history` | Last 20 predictions |
| GET | `/fields` | Input field metadata |

### Example Request

```bash
curl -X POST https://stellar-analytics-backend.onrender.com/predict/full \
  -H "Content-Type: application/json" \
  -d '{
    "koi_period": 9.49,
    "koi_duration": 2.96,
    "koi_depth": 615.8,
    "koi_impact": 0.15,
    "koi_model_snr": 35.8,
    "koi_num_transits": 142,
    "koi_ror": 0.022,
    "teff": 5455,
    "logg": 4.47,
    "feh": 0.12
  }'
```

### Example Response

```json
{
  "classification": {
    "prediction": "CONFIRMED",
    "confidence": 97.6,
    "probabilities": {
      "CONFIRMED": 97.6,
      "FALSE_POSITIVE": 2.4
    }
  },
  "regression": {
    "predicted_radius": 2.25,
    "planet_category": "Mini-Neptune"
  },
  "timestamp": "2026-03-13T10:30:00"
}
```

---

## 📊 Input Parameters

| Parameter | Description | Range |
|-----------|-------------|-------|
| `koi_period` | Orbital period (days) | 0.5 – 1000 |
| `koi_duration` | Transit duration (hours) | 0.5 – 24 |
| `koi_depth` | Transit depth (ppm) | 10 – 100,000 |
| `koi_impact` | Impact parameter | 0 – 1.5 |
| `koi_model_snr` | Signal-to-noise ratio | 0 – 2000 |
| `koi_num_transits` | Number of transits | 1 – 5000 |
| `koi_ror` | Planet/star radius ratio | 0.001 – 0.9 |
| `teff` | Star temperature (K) | 2500 – 10000 |
| `logg` | Surface gravity (log g) | 1 – 5.5 |
| `feh` | Metallicity (dex) | -2.5 – 1.0 |

---

## 🪐 Planet Categories

| Category | Radius Range |
|----------|-------------|
| Rocky / Earth-like | < 1.25 R⊕ |
| Super-Earth | 1.25 – 2.0 R⊕ |
| Mini-Neptune | 2.0 – 4.0 R⊕ |
| Neptune-like | 4.0 – 10.0 R⊕ |
| Gas Giant / Jupiter-like | > 10.0 R⊕ |

---

## 👥 Team

| Name | Role |
|------|------|
| **Aryan Sinha** | Frontend & API |
| **Mihir Waghmare** | ML & Backend |
| **Anushka** | EDA & Analysis |

**Indian Institute of Technology (BHU) Varanasi**

---

## 📚 References

1. [NASA Exoplanet Archive](https://exoplanetarchive.ipac.caltech.edu/)
2. [Kepler Object of Interest — Wikipedia](https://en.wikipedia.org/wiki/Kepler_object_of_interest)
3. [Methods of Detecting Exoplanets](https://en.wikipedia.org/wiki/Methods_of_detecting_exoplanets)

---

*Stellar Analytics · TECHNEX '26 · IIT BHU*

