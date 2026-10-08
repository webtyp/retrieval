# Agent Guide — `webtyp/retrieval`

Constraints for agents working on this library. **Read this before any change.**
The current work order, when one exists, is [docs/PLAN.md](docs/PLAN.md). The master index of
the semantic-search work is [docs/SEMANTIC_SEARCH_MASTER_PLAN.md](docs/SEMANTIC_SEARCH_MASTER_PLAN.md).
The ecosystem plan is
[`agent/docs/AGENT_ECOSYSTEM_MASTER_PLAN.md`](https://github.com/webtyp/agent/blob/main/docs/AGENT_ECOSYSTEM_MASTER_PLAN.md).

## What this library is

Chunking, ingestion and search over `embed` and `vectordb`. It must never:

- import `webtyp/agent` or `webtyp/agentmemory` (they use this library, not the reverse),
- choose or construct an embedding model (it receives an `embed.Embedder`),
- re-implement vector math, storage, tokenization or the encoder (each has its own repository).

**Its primary runtime is a browser tab compiled with TinyGo.**

## The builds that define "done"

```bash
go vet ./...
gotest
gotest -tinygo
GOOS=js GOARCH=wasm go build ./...
```

## Never import these

| Never | Use instead | Why |
|---|---|---|
| `fmt`, `errors`, `strings`, `strconv` | `webtyp.com/fmt` | isomorphic, small under TinyGo |
| `context` (stdlib) | `webtyp.com/context` | every webtyp API takes `*context.Context` |
| `encoding/json` | `webtyp.com/json` | reflection JSON costs ~1 MB of wasm |
| `time` | `webtyp.com/time` | |
| `database/sql` | `webtyp.com/storage` through `vectordb` | the isomorphism lives in `orm`/`ddl` (D7) |
| `sort` | a hand-written sort | reflection is a size tax under TinyGo |
| `map[K]V` | a slice | TinyGo's map runtime is a size tax |
| `os`, `log`, `net/http` | inject it / `webtyp.com/fetch` | a library never touches the process environment |

## Common mistakes to avoid

- Promoting a figure marked `[inv]` (unverified research) to a design decision without going
  back to the primary source. `SEMANTIC_SEARCH_MASTER_PLAN.md` D0 records the time this
  happened, and the fix.
- Chunking by characters. The limit is 256 **tokens of the embedding model**.
