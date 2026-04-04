# HumanizeAI

HumanizeAI is a single-file web application for rewriting text with a multi-agent pipeline.

## Overview

The app runs a three-agent workflow:

1. Agent 1 (Detector) identifies AI-like sections.
2. Agent 2 (Humanizer) rewrites content to sound more natural.
3. Agent 3 (Verifier) checks meaning preservation.

It supports multiple providers (including local models), iteration history, diff comparison, and export options.

## Project Files

- `humanizeai_v2 (1).html` - Main self-contained application.
- `README.md` - Project documentation.

## Run Locally

1. Open `humanizeai_v2 (1).html` in a modern browser.
2. Configure model providers from the in-app Models panel.
3. Load or write text, then run the pipeline.

## Security Notes

- Do not commit API keys or secrets.
- Use local browser storage carefully on shared machines.
- Prefer environment-specific key handling if you later split this into a backend/frontend architecture.

## License

No license file is currently included.
