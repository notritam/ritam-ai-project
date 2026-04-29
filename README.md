# Ritam AI — Intelligent Decision Tools

Two AI-powered web tools: **ScentAI** (fragrance recommendations) and **DriveIQ** (car deal analysis & negotiation tactics).

## Project Structure

```
ritam-ai-project/
├── frontend/                  ← Deploy to GitHub Pages
│   ├── index.html             ← Landing page
│   ├── fragrance-ai.html      ← ScentAI — Fragrance advisor
│   └── car-ai.html            ← DriveIQ — Car deal analyzer
│
├── backend/                   ← Deploy to Render / Railway
│   ├── server.js              ← Express API server
│   ├── package.json           ← Dependencies
│   └── .env.example           ← Environment variable template
│
└── README.md
```

## Features

### ScentAI (Fragrance Advisor)
- Personalized fragrance recommendations via conversational AI
- Preference sidebar: occasion, season, gender, budget, and scent notes
- Clone/dupe suggestions for expensive fragrances
- Sophisticated beige/cream design with serif typography

### DriveIQ (Car Deal Analyzer)
- Instant deal analysis: fair market value, verdict, and red flags
- Word-for-word negotiation scripts to use at the dealership
- Vehicle detail input panel with priority selection
- Dark futuristic design with blue accent lighting

## Quick Start

1. `cd backend && npm install`
2. Copy `.env.example` to `.env` and add your OpenAI API key
3. `npm start` to run the backend on port 3000
4. Open `frontend/index.html` in your browser

## Deployment

- **Frontend** → GitHub Pages
- **Backend** → Render.com or Railway.app
- Update `%%BACKEND_URL%%` in both HTML files with your deployed backend URL

## Tech Stack

Vanilla HTML/CSS/JS | Node.js + Express | OpenAI API (gpt-4o-mini)

Built by Ritam — MIT License
