# LinkedIn Post Agent

A React app that generates LinkedIn posts for Assaf Antebi (Enterprise Account Manager at Cast AI) using the Claude API.

## Stack
- Vite + React
- Claude API (`claude-sonnet-4-20250514`)

## Setup
1. Clone the repo
2. `npm install`
3. Copy `.env.example` to `.env` and add your Anthropic API key
4. `npm run dev`

## Environment Variables
```
VITE_ANTHROPIC_API_KEY=your_key_here
```

## Features
- 5 pre-defined K8s/GPU/cloud news topics
- 4 tone options (Thought Leader, Practitioner, Storyteller, Evangelist)
- Live LinkedIn post preview with typewriter effect
- Quality checks (word count, hashtags, @Cast AI tag, no em dashes)
- Audit logs tab
- Copy to clipboard
