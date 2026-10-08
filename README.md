# retrieval
<img src="docs/img/badges.svg">

Browser-native retrieval for webtyp: split documents into chunks, embed them, store them, and
find the chunks that answer a question. It all runs in the browser, in Go compiled with TinyGo,
over `webtyp/embed` and `webtyp/vectordb`. This repository also owns the semantic-search master
plan.

> **STATUS (remove this note when the first plan lands):** no code yet. The first plan
> (chunking) waits for `embed` v0.3.0 (`CountTokens`) and the open decision listed in
> `docs/ARCHITECTURE.md`.

## Getting started

| I want to… | Read |
|---|---|
| understand how browser semantic search was built | [Semantic search master plan](docs/SEMANTIC_SEARCH_MASTER_PLAN.md) |
| know where this library sits and what it will do | [Architecture](docs/ARCHITECTURE.md) |
| know why this embedding model was chosen | [Embedding model choice](docs/SMALL_MODEL_FOR_EMBEDING.md) |

## Documentation

- [Architecture](docs/ARCHITECTURE.md)
- [Semantic search master plan](docs/SEMANTIC_SEARCH_MASTER_PLAN.md)
- [Embedding model choice](docs/SMALL_MODEL_FOR_EMBEDING.md)
- [Cloudflare Workers AI](docs/CLOUDFLARE_AI_WORKER.md)
- [History: semantic search wave](docs/history/SEMANTIC_SEARCH_WAVE.md)
- [History: WebGPU encoder](docs/history/WEBGPU_ENCODER.md)
- [Agent guide](AGENTS.md)
