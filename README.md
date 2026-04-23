# Perplexity AI Toolkit

> **Unmaintained.** Perplexity's API is OpenAI-compatible; use the [`openai`](https://github.com/openai/openai-python) SDK pointed at `https://api.perplexity.ai/`.

I've always preferred pair programming with LLMs from the terminal over copy-pasting from browser chats. Web UIs hit rate limits, lose context across tabs, and break flow when I'm moving code back and forth. Perplexity opened their API early January 2024 and the pitch was unique: real-time web search as a first-class mode, not an afterthought. I wanted chat and search behind one CLI, streaming, system prompts, and the full parameter surface. So I built this for myself.

Python wrapper and CLI for Perplexity's Sonar models, with real-time online search.

## Install

```bash
git clone https://github.com/ramonclaudio/perplexity-ai-toolkit.git
cd perplexity-ai-toolkit
pip install -r requirements.txt
```

## Configuration

Get an API key at https://www.perplexity.ai/. Set via env var, `.env`, or pass directly:

```bash
export PERPLEXITY_API_KEY=your_api_key
```

## CLI

```bash
# Chat
python cli.py --chat

# Online search (single query, no multi-turn)
python cli.py --search --query "What is today's date?"
```

Type `exit` or `quit` to leave chat.

## Python

```python
from perplexity import Chat, Search

Chat().run()
Search().run(query="What is today's date?")
```

Search mode is limited to `-online` Sonar models, which don't support multi-turn.

## Options

| Description | CLI | Python |
| --- | --- | --- |
| Chat mode | `--chat` | `Chat()` |
| Search mode | `--search` | `Search()` |
| Search query | `--query` | `query=` |
| Prompt | `--prompt` | `prompt=` |
| API key | `--api_key` | `api_key=` |
| Model | `--model` | `model=` |
| Streaming | `--stream` | `stream=True` |
| System prompt | `--system_prompt` | `system_prompt=` |
| Max tokens | `--max_tokens` | `max_tokens=` |
| Temperature | `--temperature` | `temperature=` |
| Top-p | `--top_p` | `top_p=` |
| Top-k | `--top_k` | `top_k=` |
| Presence penalty | `--presence_penalty` | `presence_penalty=` |
| Frequency penalty | `--frequency_penalty` | `frequency_penalty=` |

## Models

### Online (search)

| Model | Params | Context |
| --- | --- | --- |
| `llama-3.1-sonar-small-128k-online` | 8B | 127072 |
| `llama-3.1-sonar-large-128k-online` | 70B | 127072 |
| `llama-3.1-sonar-huge-128k-online` | 405B | 127072 |

Online models don't respect full system prompts. Use system prompts for style/tone/language only.

### Chat

| Model | Params | Context |
| --- | --- | --- |
| `llama-3.1-sonar-small-128k-chat` | 8B | 131072 |
| `llama-3.1-sonar-large-128k-chat` | 70B | 131072 |

### Open-source

| Model | Params | Context |
| --- | --- | --- |
| `llama-3.1-8b-instruct` | 8B | 131072 |
| `llama-3.1-70b-instruct` | 70B | 131072 |

## License

MIT
