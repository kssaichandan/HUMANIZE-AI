# HumanizeAI

> **🌐 Live app:** https://humanize-ai-text.kssaichandan.workers.dev

**🌐 Live app:** https://humanize-ai-text-kd2b.onrender.com

> **📦 Source code:** https://github.com/kssaichandan/HUMANIZE-AI

**HumanizeAI** is a single-file, zero-install web app that rewrites AI-sounding text into natural, human prose using a self-correcting **three-agent pipeline**. Everything runs in your browser — your text and API keys never leave your machine except to go directly to the model provider you choose.

> Open `Humanize AI.html` in any modern browser and you're running. No build step, no server, no account.

---

## How it works

Your document passes through a loop of three AI agents that critique and improve each other's work:

1. **Detector** — scores how "AI-written" the text reads and flags the giveaway passages.
2. **Humanizer** — rewrites the flagged text to sound natural while preserving meaning and facts.
3. **Verifier** — checks the rewrite still means the same thing and re-scores it.

After each rewrite the Detector runs again on the new text, so the app *measures* its own improvement instead of guessing. The loop repeats until **both** gates are satisfied:

- **Meaning preserved** ≥ your meaning threshold, **and**
- **AI score** ≤ your AI-score threshold.

If a run hits the iteration limit without clearing both gates, the app marks the best iteration (★) and offers to accept it.

---

## Features

### Pipeline
- Iterative Detector → Humanizer → Verifier loop (1–20 iterations).
- Two-gate stop condition (meaning **and** AI score must both pass).
- "Already human" short-circuit — skips rewriting if the text is already clean.
- Pause / resume / stop mid-run, and per-agent re-run.
- Live token-by-token streaming of each agent's output.

### Models & providers
- Built-in support for **OpenAI, Anthropic (Claude), Google Gemini, Groq, Mistral, and Together AI**.
- Any **OpenAI-compatible endpoint** via the Custom provider (OpenRouter, LM Studio, llama.cpp, vLLM, etc.).
- **Local models** through Ollama — scan, select, and auto-assign across all three agents.
- Mix and match: a different model for each agent if you like.
- One-click connection test for each provider.

### External AI detectors (optional)
- Plug in a real detector API — Turnitin-compatible, GPTZero / ZeroGPT-compatible, Copyleaks-compatible, or any custom/local endpoint — and assign it to the Detector agent for authoritative scoring.
- A built-in **statistical AI signal** (burstiness, vocabulary diversity, AI-phrase density) runs locally with no API call, and warns you when it diverges sharply from the model's score.

### Rewrite style controls
Shape the Humanizer's output with three dropdowns:
- **Intensity** — *Light (targeted)* edits only the flagged passages, *Standard* rewrites the whole document, *Aggressive* freely restructures.
- **Reading level** — Default / High school / University / Doctorate.
- **Purpose** — Essay, Research paper, Patent, Technical report, Business report, Blog post, Email, or Marketing. Formal options push toward precise, objective, contraction-free prose; casual ones toward conversational writing.

### Input & output
- Input by **upload** (`.txt`, `.md`, `.pdf`, `.docx`), **paste**, or **write** — drag-and-drop supported.
- Handles long documents automatically (chunked rewriting when needed).
- Side-by-side diff to compare the original against any iteration.
- Full iteration history with per-run scores and an AI-score trend sparkline.
- Export the result as `.txt`, `.md`, or `.docx`, or export/import the whole session as JSON.

### Privacy
- 100% client-side. **No server, no tracking, no analytics, no accounts.**
- API keys are stored only in your browser's `localStorage` and are sent only to the provider's own endpoint.
- Key inclusion in session exports is **off by default** and requires explicit confirmation.

---

## Getting started

1. **Open the app.** Double-click `Humanize AI.html`, or for local model/detector endpoints serve the folder first:
   ```bash
   python -m http.server 8000
   # then visit http://localhost:8000/Humanize%20AI.html
   ```
2. **Add a model.** Open the **Models** panel, pick a provider, paste your API key (or point at a local Ollama/Custom endpoint), and assign models to the three agents.
3. *(Optional)* **Add a detector.** In **Models → Detector APIs**, configure an external detector and assign it to Agent 1 for real-world scoring.
4. **Add your text.** Upload, paste, or write it.
5. **Tune settings** *(optional)* — iteration cap, meaning threshold, AI-score threshold, and rewrite style.
6. **Run** and review the results, diff, and history.

### Where to get free API keys
- **Groq** — fast Llama/Mixtral models, generous free tier (`console.groq.com`).
- **Google Gemini** — free tier with very large context (`aistudio.google.com`).
- **Mistral** — free tier (`console.mistral.ai`).
- **Ollama** — fully local and free if you have the hardware (`ollama.com`).

---

## Hosting

The app is a single static HTML file, so it can be hosted on any static host. On every host the only "build" is copying the app to `index.html`:

- **Build command:** `mkdir -p public && cp "Humanize AI.html" public/index.html`
- **Build output directory:** `public`

### Cloudflare Pages (recommended — clean free URL)

1. [dash.cloudflare.com](https://dash.cloudflare.com) → **Workers & Pages → Create → Pages → Connect to Git** → select this repo.
2. **Project name** `humanize-ai-text`, **production branch** `main`, **framework preset** `None`.
3. Enter the build command and output directory above → **Save and Deploy**.
4. Live at **https://humanize-ai-text.kssaichandan.workers.dev** — Cloudflare now serves static deploys on `<project>.<account>.workers.dev` and gives the exact project name you choose (no random suffix).

### Render (alternative)

This repo also includes a Render blueprint (`render.yaml`): in the [Render](https://render.com) dashboard, **New + → Blueprint → connect this repo**. Works the same way, but note Render appends a random suffix to free `.onrender.com` URLs (e.g. `humanize-ai-text-kd2b.onrender.com`).

The app needs no backend — API calls go directly from the visitor's browser to whichever model provider they configure.

## Project structure

- `Humanize AI.html` — the entire self-contained application (UI, pipeline, and logic in one file).
- `render.yaml` — Render blueprint for free static hosting.
- `README.md` — this file.

---

## License

No license file is currently included; all rights reserved by the author.
