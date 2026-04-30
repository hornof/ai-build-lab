# AI Project HQ

A single-file productivity dashboard for tracking AI projects, session logs, and feature backlogs — with a Claude-powered "Suggest Next Feature" button.

![Dark mode dashboard with projects, session log, backlog, and AI suggest panel]

## Features

- **Projects** — track name, status (Active / Paused / Planning / Done), and notes
- **Session Log** — daily entries for what you built and what's next
- **Feature Backlog** — per-project feature list with priority and status
- **AI Suggest** — Claude analyzes your project state and recommends what to build next; one click saves the recommendation to your backlog

Data is stored server-side in `data.json` — every browser pointing at the local server sees the same state. Nothing leaves your machine except the AI suggest call, which the proxy forwards to Anthropic.

## Setup

### 1. Install dependencies

```bash
npm install
```

### 2. Add your Anthropic API key

Create a `.env` file in the project root (or edit the one that's there):

```
ANTHROPIC_API_KEY=sk-ant-...your-key-here...
```

Get a key at [console.anthropic.com](https://console.anthropic.com) → API Keys → Create Key. You only see the full key once, so copy it immediately.

### 3. Start the server

```bash
npm start
```

You should see:

```
AI Project HQ running at http://localhost:3001/dashboard.html
```

### 4. Open the dashboard

Open **http://localhost:3001/dashboard.html** in your browser.

> The server must be running for the dashboard to load or save your data — projects, sessions, and backlog all live in `data.json` on disk, accessed via the local API.

## Project structure

```
dashboard.html   — the entire frontend (vanilla HTML/CSS/JS)
server.js        — Express server: serves the dashboard, persists data, proxies AI requests
data.json        — your projects, sessions, and backlog (auto-created, gitignored)
.env             — your API key (never committed)
package.json     — dependencies (express, dotenv)
```

## Tech

- Vanilla HTML/CSS/JS, no frameworks
- Node.js + Express server (serves frontend, persists `data.json`, proxies AI calls)
- Anthropic API (claude-sonnet-4-6)
