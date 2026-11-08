# Install - instructions for an AI agent

This repo is the index for the agent_utils platform. There is no server here to install.

agent_utils is two *hosted* MCP servers on `mcp.agent-utils.ai`, sharing **one account, one
token, and one credit pool**. To install both:

```bash
TOKEN=sk_$(openssl rand -hex 32)          # the token IS the account; save it
claude mcp add --scope user --transport http agent-utils-swarm \
  https://mcp.agent-utils.ai/swarm --header "Authorization: Bearer $TOKEN"
claude mcp add --scope user --transport http agent-utils-extensions \
  https://mcp.agent-utils.ai/extensions --header "Authorization: Bearer $TOKEN"
```

Use **the same token** for both.

| Server | Endpoint | Services |
|---|---|---|
| `swarm` | `https://mcp.agent-utils.ai/swarm` | memory, mutex (locks), task board, pub/sub, idempotency, webhook inbox |
| `extensions` | `https://mcp.agent-utils.ai/extensions` | math (expression evaluation), units (56 quantities) |

No signup, no dashboard, no card. The first call auto-provisions a trial (1,000 credits).
`tools/list` is unauthenticated, so either server can be inspected before use:

```bash
curl -s -X POST https://mcp.agent-utils.ai/swarm -H 'Content-Type: application/json' \
  -d '{"jsonrpc":"2.0","id":1,"method":"tools/list"}'
```

Platform index: <https://mcp.agent-utils.ai/llms.txt>. Terms:
<https://mcp.agent-utils.ai/legal.txt>.

The hosted services are a commercial product and are not open-source; the client libraries
indexed here are MIT.
