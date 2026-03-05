# LinkedIn Post Agent — Cast AI

An AI-powered internal tool that ghostwrites LinkedIn posts in your voice, focused on Kubernetes, GPU management, AI infrastructure, and cloud cost optimization topics.

Built with React + Vite, powered by the [Claude API](https://www.anthropic.com/).

---

## Features

| Feature | Description |
|---|---|
| **Passphrase Lock** | Password-protected entry screen; unlock state is remembered in `localStorage` so you don't re-enter on reload |
| **Voice Profile Setup** | First-time setup screen collects your Display Name, Job Title, Voice Patterns, and Sample Post Hooks; editable any time via the avatar menu |
| **Dynamic Topic Discovery** | Claude generates 5 fresh, trending topics in the K8s/GPU/cloud ecosystem on every load — no stale hardcoded content |
| **🔥 Find New Hot Topics** | One-click button to refresh the topic set at any time |
| **4 Tone Modes** | Thought Leader, Practitioner, Storyteller, Evangelist |
| **Live Preview** | LinkedIn-style post card with typewriter streaming effect |
| **Quality Checker** | Real-time flags for word count, hashtag count, `@Cast AI` tag, and em-dash violations |
| **Regenerate** | Re-run with a randomly-chosen alternate tone in one click |
| **Audit Logs** | Full event log of every generation, copy, error, and topic load |

---

## Tech Stack

- **React 19** — UI
- **Vite 7** — build tool and dev server
- **Claude API** (`claude-sonnet-4-6`) — topic generation and post ghostwriting
- **No backend** — all API calls go directly from the browser using `anthropic-dangerous-direct-browser-access`

---

## Quickstart

### Prerequisites

- Node.js 18+
- An Anthropic API key (see steps below)

#### How to create an Anthropic API key

1. Go to [console.anthropic.com](https://console.anthropic.com/) and sign up or log in
2. Navigate to **API Keys** in the left sidebar (or go to **Settings → API Keys**)
3. Click **Create Key**
4. Give your key a name (e.g. `linkedin-agent`) and click **Create Key**
5. **Copy the key immediately** — it is only shown once
6. Store it safely; you will paste it into `.env` in step 3 below

### 1. Clone the repo

```bash
git clone https://github.com/assaf-spec/linkedin-agent.git
cd linkedin-agent
```

### 2. Install dependencies

```bash
npm install
```

### 3. Configure environment variables

```bash
cp .env.example .env
```

Open `.env` and fill in your values:

```env
VITE_ANTHROPIC_API_KEY=sk-ant-api03-...
VITE_ACCESS_PASSPHRASE=your-secret-passphrase
```

> **Never commit `.env`** — it is already in `.gitignore`.

### 4. Start the dev server

```bash
npm run dev
```

Open [http://localhost:5173](http://localhost:5173) (Vite may pick a higher port if 5173 is in use — check the terminal output).

### 5. First-time setup inside the app

1. Enter the passphrase you set in `.env`
2. Fill in your **Display Name**, **Job Title**, voice patterns, and sample post hooks
3. Click **Save Profile** — your profile is persisted in `localStorage`

---

## Usage

```
1. Enter passphrase  →  unlocked state persists in localStorage
2. First time only: fill in Display Name, Job Title, Voice Patterns, Sample Hooks → Save Profile
3. App loads  →  Claude fetches 5 hot trending topics automatically
4. Pick a topic card
5. Choose a tone: Thought Leader / Practitioner / Storyteller / Evangelist
6. Click ✨ Generate Post
7. Review the live preview and Quality Check panel
8. Click 📋 Copy Post  →  paste into LinkedIn
```

To get a brand-new batch of topics at any time, click **🔥 Find New Hot Topics** below the topic list.

To lock the app or edit your voice profile, click the avatar initials in the top-right corner.

---

## Project Structure

```
linkedin-agent/
├── src/
│   ├── App.jsx          # Entire application (single-file architecture)
│   └── main.jsx         # React entry point
├── index.html
├── vite.config.js
├── .env                 # Local secrets — never commit
├── .env.example         # Safe template — commit this
└── package.json
```

### Key components and functions in `App.jsx`

| Name | Purpose |
|---|---|
| `PassphraseScreen` | Lock screen rendered before the main app; validates `VITE_ACCESS_PASSPHRASE` |
| `ProfileSetupScreen` | First-time (and editable) form for Display Name, Job Title, Voice Patterns, Sample Hooks |
| `fetchTopics()` | Calls Claude to generate 5 trending topic objects as JSON |
| `gen(topicObj, tone, voice)` | Calls Claude to write a LinkedIn post using the voice profile as the system prompt |
| `buildPrompt(topicObj, tone)` | Constructs the user prompt from topic data and tone |
| `sys(voice)` | Builds the system prompt from the user's voice profile |
| `loadTopics` | `useCallback` — manages loading/error state for topic fetching |
| `generate` | `useCallback` — manages loading/error state for post generation |

---

## Environment Variables

| Variable | Required | Description |
|---|---|---|
| `VITE_ANTHROPIC_API_KEY` | Yes | Anthropic API key from [console.anthropic.com](https://console.anthropic.com/) |
| `VITE_ACCESS_PASSPHRASE` | Yes | Lock-screen passphrase; once entered correctly, the unlocked state is saved in `localStorage` |

---

## Scripts

| Command | Description |
|---|---|
| `npm run dev` | Start dev server with HMR |
| `npm run build` | Production build to `dist/` |
| `npm run preview` | Preview the production build locally |
| `npm run lint` | Run ESLint |

---

## Build for Production

```bash
npm run build
```

Output goes to `dist/`. Deploy to any static host — Vercel, Netlify, S3, GitHub Pages, etc.

> **Security note:** `VITE_ANTHROPIC_API_KEY` is embedded in the client bundle. This is intentional for an internal-only tool protected by a passphrase. For a public-facing deployment, route API calls through a backend proxy instead.

---

## Customising the Voice Profile

The voice profile is editable at any time via **avatar initials (top-right) → Edit Voice Profile**. It has four fields:

- **Display Name** — your name as it appears in the post preview (e.g. `Assaf Antebi ☁️`)
- **Job Title** — injected into Claude's system prompt (e.g. `Enterprise Account Manager at Cast AI`)
- **Voice Patterns** — writing rules the AI must follow (one per line)
- **Sample Post Hooks** — real opening lines from your past posts used to match your voice (one per line)

All fields are stored in `localStorage` and injected into every Claude system prompt.
