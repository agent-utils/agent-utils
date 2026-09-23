# Install — instructions for an AI agent

This repo is the index for the agent_utils platform. There is no server here to install.

agent_utils is a set of *hosted* MCP servers, one per subdomain of `agent-utils.ai`, sharing
**one account, one token, and one credit pool**. To install any of them:

```bash
TOKEN=sk_$(openssl rand -hex 32)          # the token IS the account; save it
claude mcp add --scope user --transport http agent-utils-memory \
  https://memory.agent-utils.ai/mcp --header "Authorization: Bearer $TOKEN"
```

Repeat with a different subdomain — and **the same token** — for each additional service.

| Service | Endpoint | Purpose |
|---|---|---|
| `memory` | `https://memory.agent-utils.ai/mcp` | persistent key-value memory |
| `mutex` | `https://mutex.agent-utils.ai/mcp` | distributed locks |
| `idempotency` | `https://idempotency.agent-utils.ai/mcp` | operation deduplication |
| `units` | `https://units.agent-utils.ai/mcp` | physical unit conversions |
| `electrical-units` | `https://electrical-units.agent-utils.ai/mcp` | electrical & electromagnetic unit conversions |
| `chemistry-units` | `https://chemistry-units.agent-utils.ai/mcp` | chemistry & analytical unit conversions |
| `thermodynamics-units` | `https://thermodynamics-units.agent-utils.ai/mcp` | thermodynamic unit conversions |
| `math` | `https://math.agent-utils.ai/mcp` | deterministic expression evaluation |
| `webhook-inbox` | `https://webhook-inbox.agent-utils.ai/mcp` | temporary pollable webhook receiver |

No signup, no dashboard, no card. The first call auto-provisions a trial (1,000 credits).
`tools/list` is unauthenticated, so any service can be inspected before use:

```bash
curl -s -X POST https://memory.agent-utils.ai/mcp -H 'Content-Type: application/json' \
  -d '{"jsonrpc":"2.0","id":1,"method":"tools/list"}'
```

Platform index: <https://agent-utils.ai/llms.txt>. Terms:
<https://accounts.agent-utils.ai/legal.txt>.

The hosted services are a commercial product and are not open-source; the client libraries
indexed here are MIT.
