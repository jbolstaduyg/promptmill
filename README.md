# promptmill

Batch prompt runner with real rate limiting and retries

## Getting started

```bash
pip install -r requirements.txt
export OPENAI_API_KEY=sk-...
```

## Highlights

- JSONL in, JSONL out: the input is streamed line by line
- 4xx fails fast; 429 and 5xx retry with jittered backoff
- Real rate limiting: sliding windows on requests/min and tokens/min
- Failures go to a sidecar file with error type, message and status
- Per-row overrides for model, system, temperature and max_tokens
- A bad input line is logged and skipped, never fatal
- Progress, token counts and a cost estimate on stderr
- Idempotent: ids already in the output are skipped on a rerun

## Usage

```bash
python batch.py prompts.jsonl -o answers.jsonl --workers 4 --rpm 300
```

## Project structure

```text
├── .github/
│   └── workflows/
│       └── ci.yml
├── docs/
│   ├── configuration.md
│   ├── faq.md
│   ├── roadmap.md
│   ├── tradeoffs.md
│   └── usage.md
├── examples/
│   └── quickstart.md
├── tests/
│   └── test_smoke.py
├── .gitignore
├── CHANGELOG.md
├── CONTRIBUTING.md
├── LICENSE
├── batch.py
├── prompts.sample.jsonl
└── requirements.txt
```

## Development

```bash
python -m venv .venv && source .venv/bin/activate
pip install -r requirements.txt
python -m pytest -q
```

## Acknowledgments

- README structure inspired by popular OSS templates
- Thanks to everyone opening issues with ideas

## License

MIT - see [LICENSE](LICENSE).
