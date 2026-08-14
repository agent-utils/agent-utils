# agent_utils

**One account for the small pieces of infrastructure AI agents keep needing** — persistent
memory, distributed locks, operation idempotency, and correct unit conversion — each an MCP
server, all behind a single token and one credit pool.

agent_utils is a hosted commercial service at **[agent-utils.ai](https://agent-utils.ai)**.
This repo is the open-source **client tooling and documentation** hub — the "start here" index
for the client libraries and examples. The service itself is closed-source; these clients only
call its public MCP/HTTP API.

## Why one account matters

A single Bearer token works across every service. All usage draws from one credit pool, one
$5 activation covers everything, and the first call auto-provisions a free trial (1,000
credits, no card). Adopt one service and the rest are already available with the token you
have. A single-purpose competitor can't match that.

## Try it in one command

```bash
TOKEN=sk_$(openssl rand -hex 32)
curl -s -X POST https://memory.agent-utils.ai/mcp \
  -H "Authorization: Bearer $TOKEN" -H "Content-Type: application/json" \
  -d '{"jsonrpc":"2.0","id":1,"method":"tools/list","params":{}}'
```

The account is created on that first call. Activate later at
`https://accounts.agent-utils.ai/setup?token=$TOKEN` ($5, raises the limit to 500,000 credits;
your trial token stays valid).

## Services

| Service | What it does | Endpoint | Spec |
|---|---|---|---|
| memory | persistent key-value memory | `memory.agent-utils.ai/mcp` | [llms.txt](https://memory.agent-utils.ai/llms.txt) |
| mutex | distributed locks | `mutex.agent-utils.ai/mcp` | [llms.txt](https://mutex.agent-utils.ai/llms.txt) |
| idempotency | operation deduplication | `idempotency.agent-utils.ai/mcp` | [llms.txt](https://idempotency.agent-utils.ai/llms.txt) |
| units | physical unit conversions | `units.agent-utils.ai/mcp` | [llms.txt](https://units.agent-utils.ai/llms.txt) |
| electrical-units | electrical & electromagnetic conversions | `electrical-units.agent-utils.ai/mcp` | [llms.txt](https://electrical-units.agent-utils.ai/llms.txt) |
| chemistry-units | chemistry & analytical conversions | `chemistry-units.agent-utils.ai/mcp` | [llms.txt](https://chemistry-units.agent-utils.ai/llms.txt) |
| thermodynamics-units | thermal & transport-property conversions | `thermodynamics-units.agent-utils.ai/mcp` | [llms.txt](https://thermodynamics-units.agent-utils.ai/llms.txt) |
| accounts | account, billing & key management for all of the above | `accounts.agent-utils.ai/mcp` | [llms.txt](https://accounts.agent-utils.ai/llms.txt) |

The conversion services use compile-time dimensional analysis, so every supported unit pair is
correct by construction — the failure mode agents have with unit math doesn't apply.

## Client libraries

Thin, zero-dependency wrappers over the MCP endpoints. One package per service per language.

| Service | TypeScript (npm) | Python (PyPI) |
|---|---|---|
| memory | [`@agent-utils/memory`](https://codeberg.org/agent-utils/agent-utils-memory-ts) | [`agent-utils-memory`](https://codeberg.org/agent-utils/agent-utils-memory-py) |

_(more services rolling out — see each service's `llms.txt` to use it directly today with any
MCP client)_

## Examples

- [Claude Code with persistent memory](https://codeberg.org/agent-utils/agent-utils-example-claude-code-memory)
- [Multi-service: memory + mutex + idempotency](https://codeberg.org/agent-utils/agent-utils-example-multi-service)

## Pricing

1 credit = $0.00001. Most operations are 15 credits ($0.00015). Trial: 1,000 credits, no card.
Activation: $5 one-time, 500,000-credit limit. Full terms:
[accounts.agent-utils.ai/legal.txt](https://accounts.agent-utils.ai/legal.txt).

## License

Client tooling in the agent_utils repos is MIT-licensed. The hosted service is a separate
commercial product and is not open-source.
