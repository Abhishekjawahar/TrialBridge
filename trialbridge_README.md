# TrialBridge

> **Helping patients and caregivers find and understand clinical trials — in plain language.**

TrialBridge is a zero-backend, browser-based application that searches ClinicalTrials.gov in real time and uses Google Gemini AI to translate complex eligibility criteria and medical language into clear, human explanations. Built as a single HTML file — no framework, no build step, no server required.

---

## 🌐 Live Demo

Open `trialbridge.html` directly in any modern browser. Add your Gemini API key to enable AI-powered plain-language explanations.

---

## ✨ Features

### 🔍 Smart Trial Search
- Searches **400,000+ registered studies** via the ClinicalTrials.gov API v2
- Filters by condition, age, location, sex, and trial phase
- Returns only actively recruiting studies
- Resolves US ZIP codes to geographic coordinates for distance calculation
- Proximity-based relevance scoring — nearest trials ranked highest

### 🤖 AI-Powered Plain Language
- **Adaptive tone** — detects whether the user is a Patient, Caregiver, or Healthcare Professional and adjusts the explanation style accordingly
- **Plain-language summaries** — converts dense medical abstracts into 2–3 clear sentences
- **Eligibility explained** — breaks down inclusion/exclusion criteria into two simple lists: who can join, who cannot
- **Doctor talking points** — generates 4 specific, relevant questions to bring to a healthcare appointment
- Powered by **Google Gemini 1.5 Flash** (free tier)

### 📊 Relevance Scoring
Each trial receives a 0–100 match score based on:
- Distance from user's ZIP code
- Trial phase (Phase 3 weighted higher)
- Recruitment status (Actively recruiting scored highest)
- Number of trial locations (more sites = more accessible)

### 🗂 Results & Filtering
- Filter cards by Phase 3, Nearby (< 50 miles), or High Match
- Each card shows phase badge, recruitment status, distance, and AI summary
- Click any card for the full detail view

### 📋 Export for Appointments
- Copy a full results summary to clipboard (all matched trials)
- Copy a single-trial appointment sheet with doctor questions
- Print-friendly layout

---

## 🚀 Getting Started

### 1. Get a free Gemini API key

1. Go to [aistudio.google.com](https://aistudio.google.com)
2. Sign in with your Google account
3. Click **Get API key → Create API key**
4. Copy the key

> The free tier includes 15 requests/minute and 1 million tokens/day — more than enough for real usage.

### 2. Add your key to the app

Open `trialbridge.html` in a text editor and replace line 3:

```javascript
const GEMINI_API_KEY = 'YOUR_GEMINI_API_KEY';
```

with your actual key:

```javascript
const GEMINI_API_KEY = 'AIzaSy...your_key_here';
```

### 3. Open in browser

```bash
open trialbridge.html
# or just double-click the file
```

No install. No server. No build step.

---

## 🛠 Technical Architecture

```
User Input (condition, age, ZIP, user type)
         ↓
ZIP → Coordinates (Zippopotam.us — free, no key)
         ↓
ClinicalTrials.gov API v2 (free, no key required)
         ↓
Relevance Scoring Engine (distance + phase + status)
         ↓
Google Gemini 1.5 Flash (free tier API)
  ├── Plain-language summary
  ├── Eligibility criteria rewrite
  └── Doctor talking points
         ↓
Rendered Results (HTML/CSS/JS — no framework)
```

### APIs Used

| API | Purpose | Cost | Auth |
|-----|---------|------|------|
| [ClinicalTrials.gov v2](https://clinicaltrials.gov/data-api/api) | Trial data | Free | None required |
| [Zippopotam.us](https://www.zippopotam.us/) | ZIP → coordinates | Free | None required |
| [Google Gemini 1.5 Flash](https://aistudio.google.com) | AI explanations | Free tier | API key |

### Key Implementation Details

- **No backend** — all API calls made directly from the browser
- **Lookahead AI loading** — top 5 results are AI-enriched in parallel using `Promise.all`
- **Graceful degradation** — if Gemini API is unavailable, raw summaries from ClinicalTrials.gov are shown instead
- **Demo mode** — app works without a Gemini API key, showing raw data with a placeholder message
- **Haversine distance** — great-circle distance calculation between ZIP centroid and trial location coordinates
- **Adaptive system prompt** — Gemini receives a different persona instruction based on user type (patient / caregiver / professional)

---

## 📁 File Structure

```
trialbridge/
├── trialbridge.html    # Entire application — self-contained single file
├── README.md           # This file
└── LICENSE             # MIT License
```

---

## 🖥 Screens

| Screen | Description |
|--------|-------------|
| **Intake** | Condition, age, ZIP input with user type selector and optional advanced fields |
| **Loading** | Live step-by-step progress feed showing API activity |
| **Results** | Scored trial cards with filtering, distance, phase, and AI summaries |
| **Detail** | Full plain-language breakdown with eligibility grid, locations, and doctor questions |

---

## ⚠️ Disclaimer

TrialBridge is an informational tool to help people discover and understand clinical trials. It does **not** provide medical advice, medical diagnosis, or treatment recommendations. All trial information is sourced directly from ClinicalTrials.gov. Always discuss clinical trial participation with a qualified healthcare provider before making any decisions.

---

## 🔮 Potential Extensions

- **Multi-condition search** — match trials relevant to patients with comorbidities
- **Saved trials** — localStorage bookmarking across sessions
- **Email export** — send trial summaries directly to a doctor
- **Eligibility pre-check** — structured questionnaire that pre-screens eligibility before showing results
- **Trial alerts** — check back for new matching trials (would require a backend)
- **Multilingual** — translate summaries into other languages via Gemini

---

## 🙏 Credits

Created by **Abhishek Jawahar**

Built with:
- [ClinicalTrials.gov API](https://clinicaltrials.gov/data-api/api) — National Library of Medicine
- [Google Gemini API](https://aistudio.google.com) — Google DeepMind
- [Instrument Serif](https://fonts.google.com/specimen/Instrument+Serif) & [DM Sans](https://fonts.google.com/specimen/DM+Sans) via Google Fonts
- [Zippopotam.us](https://www.zippopotam.us/) — ZIP code geocoding

---

## 📄 License

MIT License © 2026 Abhishek Jawahar — see [LICENSE](./LICENSE) for full text.
