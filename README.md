# agent_utils

**One account for the small pieces of infrastructure AI agents keep needing** - persistent
memory, distributed locks, a shared task board, pub/sub, operation idempotency, webhook
inboxes, exact math, and correct unit conversion - on two MCP servers, behind a
single token and one credit pool.

agent_utils is a hosted commercial service at **[agent-utils.ai](https://agent-utils.ai)**.
This repo is the open-source **client tooling and documentation** hub - the "start here" index
for the client libraries and examples. The service itself is closed-source; these clients only
call its public MCP/HTTP API.

## Why one account matters

A single Bearer token works on both servers and every service on them. All usage draws from
one credit pool, one $5 activation covers everything, and the first call auto-provisions a
free trial (1,000 credits, no card). Adopt one service and the rest are already available
with the token you have.

## Try it in one command

```bash
TOKEN=sk_$(openssl rand -hex 32)
curl -s -X POST https://mcp.agent-utils.ai/swarm \
  -H "Authorization: Bearer $TOKEN" -H "Content-Type: application/json" \
  -d '{"jsonrpc":"2.0","id":1,"method":"tools/list","params":{}}'
```

The account is created on the first tool call. Activate later at
`https://mcp.agent-utils.ai/setup?token=$TOKEN` ($5, raises the limit to 500,000 credits;
your trial token stays valid).

## Servers

| Server | Endpoint | Services |
|---|---|---|
| **swarm** - stateful coordination | `https://mcp.agent-utils.ai/swarm` | memory, mutex, task board, pub/sub, idempotency, webhook inbox |
| **extensions** - stateless capabilities | `https://mcp.agent-utils.ai/extensions` | math, units (56 quantities: general, electrical, chemistry, thermodynamics) |

Both servers also carry the account tools (`get_account`, API keys, payments, feedback).
Full spec: [llms.txt](https://mcp.agent-utils.ai/llms.txt); per service:
`https://mcp.agent-utils.ai/docs/<service>`.

The conversion tools use compile-time dimensional analysis, so every supported unit pair is
correct by construction - the failure mode agents have with unit math doesn't apply.

## Client libraries

Thin, zero-dependency wrappers over the MCP endpoints. One package per server per language.

| Server | TypeScript (npm) | Python (PyPI) |
|---|---|---|
| swarm | [`@agent-utils/swarm`](https://github.com/agent-utils/agent-utils-swarm-ts) | [`agent-utils-swarm`](https://github.com/agent-utils/agent-utils-swarm-py) |
| extensions | [`@agent-utils/extensions`](https://github.com/agent-utils/agent-utils-extensions-ts) | [`agent-utils-extensions`](https://github.com/agent-utils/agent-utils-extensions-py) |

## Examples

- [Claude Code with persistent memory](https://github.com/agent-utils/agent-utils-example-claude-code-memory)
- [Cline / Cursor / Windsurf config](https://github.com/agent-utils/agent-utils-example-cline-config)
- [LangChain with a memory backend](https://github.com/agent-utils/agent-utils-example-langchain-memory)
- [Every service on one token: idempotency + mutex + memory + task board + pub/sub](https://github.com/agent-utils/agent-utils-example-multi-service)

## Pricing

1 credit = $0.00001. Most operations are 15 credits ($0.00015). Trial: 1,000 credits, no card.
Activation: $5 one-time, 500,000-credit limit. Full terms:
[mcp.agent-utils.ai/legal.txt](https://mcp.agent-utils.ai/legal.txt).

## Contact

Questions, bugs or account issues: support@agent-utils.ai

## License

Client tooling in the agent_utils repos is MIT-licensed. The hosted service is a separate
commercial product and is not open-source.
