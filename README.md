# LinkedIn Post Agent

A React app that ghostwrites LinkedIn posts for **Assaf Antebi** (Enterprise Account Manager at Cast AI) using the Claude API.

Pick a topic, choose a tone, and get a scroll-stopping LinkedIn post in seconds — written in Assaf's voice.

---

## Features

- 5 pre-built topics around Kubernetes, GPU optimization, and cloud infrastructure
- 4 tone modes: Thought Leader, Practitioner, Storyteller, Evangelist
- Live LinkedIn-style post preview with typewriter animation
- Quality checks: word count, hashtag count, @Cast AI tag, no em dashes
- Regenerate with a random different tone
- Copy to clipboard
- Audit logs tab tracking all generation events

## Stack

- [Vite](https://vitejs.dev/) + [React](https://react.dev/)
- [Claude API](https://docs.anthropic.com/) (`claude-sonnet-4-20250514`)

## Getting Started

### 1. Clone the repo

```bash
git clone https://github.com/assaf-spec/linkedin-agent.git
cd linkedin-agent
```

### 2. Install dependencies

```bash
npm install
```

### 3. Add your API key

Create a `.env` file in the project root:

```
VITE_ANTHROPIC_API_KEY=your_anthropic_api_key_here
```

Get your key at [console.anthropic.com](https://console.anthropic.com).

### 4. Run the app

```bash
npm run dev
```

Open [http://localhost:5173](http://localhost:5173).

## Usage

1. **Pick a topic** — choose from 5 K8s/GPU/cloud news topics
2. **Choose a tone** — Thought Leader, Practitioner, Storyteller, or Evangelist
3. **Generate** — Claude writes a post in Assaf's voice
4. **Copy** — paste directly into LinkedIn

## Security Note

Never commit your `.env` file. It is already excluded via `.gitignore`.
