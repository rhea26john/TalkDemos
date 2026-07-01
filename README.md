Live Demo given during the talks
# Media Summarizer — AI Evaluation Demo

A Jupyter notebook that demonstrates a **4-layer evaluation pipeline** for an LLM-powered news summarizer. Gemini generates bullet-point summaries; each summary is then validated by progressively more expensive checks, with Claude acting as the final LLM judge.

## What it does

| Layer | Method | Cost |
|-------|--------|------|
| 1. Deterministic | Structural rules (word count, bullet points) | Free |
| 2. Heuristics | Named-entity coverage, repetition detection | Free |
| 3. Golden dataset | Cosine similarity against human references | Free (local model) |
| 4. LLM-as-judge | Claude scores faithfulness, coherence, relevance | API call |

The pipeline **short-circuits on the first failure** — the LLM judge is only called if all cheaper layers pass.

## Prerequisites

- Python 3.9+
- A Gemini API key (for summarization)
- An Anthropic API key (for the LLM judge)

## Getting your API keys

### Gemini (Google AI Studio)

1. Go to [aistudio.google.com](https://aistudio.google.com)
2. Sign in with your Google account
3. Click **Get API key** in the left sidebar
4. Click **Create API key** and copy it

### Claude (Anthropic)

1. Go to [console.anthropic.com](https://console.anthropic.com)
2. Sign up or log in
3. Navigate to **API Keys** in the left sidebar
4. Click **Create Key**, give it a name, and copy it

> Note: Anthropic requires a paid account to use the API. You can add credits at [console.anthropic.com/settings/billing](https://console.anthropic.com/settings/billing).

## Setup

**1. Clone the repo and install dependencies**

```bash
pip install -r requirements.txt
python -m spacy download en_core_web_sm
```

**2. Create a `.env` file** in the project root with your keys:

```
GEMINI_API_KEY=your_gemini_key_here
ANTHROPIC_API_KEY=your_anthropic_key_here
```

**3. Open the notebook**

```bash
jupyter notebook eval_demo.ipynb
```

**4. Run all cells top to bottom** (`Kernel > Restart & Run All`)

Each section includes a passing and a failing demo so you can see exactly where and why the pipeline stops.

## Configuration

You can override the default models via `.env`:

```
GEMINI_MODEL=gemini-2.5-flash
CLAUDE_MODEL=claude-sonnet-4-6
```

## Project structure

```
media-summarizer/
├── eval_demo.ipynb   # Main notebook
├── requirements.txt  # Python dependencies
└── .env              # API keys (create this yourself, do not commit)
```
