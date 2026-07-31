AI Site Intelligence Assistant

A 6-Week Project — Mobile App + Open-Source LLM for Construction Site Progress

Two learning outcomes drive everything here:
(1) build a real Flutter mobile app, and (2) use + deploy open-source LLMs.

System Architecture:
            ┌──────────────────────── FLUTTER APP ────────────────────────┐
                     │  Worker view: text / voice / photo / document upload         │
                     │  Owner view: dashboard, cost/progress charts,                │
                     │              RAG chat ("ask about any site")                 │
                     └───────────────────────────┬─────────────────────────────────┘
                                                  │  REST (HTTPS)
                                                  ▼
        ┌──────────────────────────── FastAPI BACKEND (Python) ───────────────────────────┐
        │                                                                                   │
        │  Ingest ──► Whisper (speech-to-text) ──► LLM extract ──► structured JSON          │
        │                                              │                                    │
        │  Model client: OpenRouter (default)  ◄──────►│  local Ollama (fallback)           │
        │                                              │                                    │
        │  RAG: docs ──► chunk ──► embed (nomic) ──► ChromaDB ──► retrieve ──► LLM answer    │
        └───────────┬──────────────────────────────┬──────────────────────────────────────┘
                    ▼                                ▼
              ┌───────────┐                   ┌───────────┐
              │  MongoDB  │                   │ ChromaDB  │
              │ (updates, │                   │ (document │
              │  costs)   │                   │  vectors) │
              └───────────┘                   └───────────┘
