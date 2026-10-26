# Claude API Course (Powered by Gemini API)

This repository contains exercises and projects completed while following the [Building with the Claude API](https://academy.claude.com/courses/building-with-the-claude-api) course by Anthropic Academy.

> **Note**: Claude does not offer a free API key, so every exercise here is ported to the **Google Gemini API** (`google-genai`). The patterns are the same (system prompts, streaming, tool use, structured output) — only the SDK calls differ.

## Lessons

| # | Notebook | Topic | Claude course |
|---|----------|-------|---------------|
| 01 | `01_making_a_request.ipynb` | First request, token usage | Lesson 1 |
| 02 | `02_multi_turn_conversations.ipynb` | Conversation history, native chat session | Lesson 2 |
| 03 | `03_system_prompts.ipynb` | Shaping behavior with `system_instruction` | Lesson 3 |
| 04 | `04_temperature.ipynb` | Predictable vs. creative sampling | Lesson 4 |
| 05 | `05_response_streaming.ipynb` | Streaming chunks, timings, assembled message | Lesson 7 |

Course numbering is kept from the original lessons, which is why streaming is Lesson 7.

## Setup

Requires **Python 3.12** and a [Gemini API key](https://aistudio.google.com/apikey).

### Windows (cmd)

```cmd
py -3.12 -m venv venv
venv\Scripts\activate.bat
python -m pip install google-genai python-dotenv ipykernel
python -m ipykernel install --user --name gemini-api-course --display-name "Python (gemini-api-course)"
copy .env.example .env
```

### macOS / Linux

```bash
python3 -m venv venv
source venv/bin/activate
pip install google-genai python-dotenv ipykernel
python -m ipykernel install --user --name gemini-api-course --display-name "Python (gemini-api-course)"
cp .env.example .env
```

Then put your key in `.env`:

```
GEMINI_API_KEY=your_gemini_api_key_here
```

Open the notebooks and select the **Python (gemini-api-course)** kernel, then Run All. `.env` and `venv/` are gitignored, so the key is never committed.

## Claude → Gemini cheat sheet

| Claude API | Gemini API |
|---|---|
| `client.messages.create(...)` | `client.models.generate_content(...)` |
| `role: "assistant"` | `role: "model"` |
| `content: "..."` | `parts: [{"text": ...}]` |
| `system=` | `config.system_instruction` |
| `max_tokens` | `config.max_output_tokens` |
| `temperature` (0–1) | `config.temperature` (0–2) |
| `stream=True` + named events | `generate_content_stream()` + response chunks |
| `stream.text_stream` | yield `chunk.text` from each chunk |
| `stream.get_final_message()` | accumulate `chunk.text` manually |
| `client.messages.stream(...)` | `client.models.generate_content_stream(...)` |
