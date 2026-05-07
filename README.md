![PyPI](https://img.shields.io/pypi/v/synapse-layer)
![License](https://img.shields.io/badge/license-Apache%202.0-blue)
![Status](https://img.shields.io/badge/status-beta-yellow)

# Synapse Layer — Memory Skill

> **RAG retrieves. Synapse remembers.**

**Persistent memory infrastructure for AI agents — AES-256-GCM encrypted at rest, semantic search, MCP-native.**

Synapse Layer is open-source persistent memory infrastructure for AI agents and assistants. Memories are encrypted at rest with AES-256-GCM, indexed via pgvector HNSW for semantic recall, and exposed through MCP JSON-RPC for native integration with Claude, GPT, Gemini, and any MCP-compatible client. Apache 2.0 licensed.

---

## The Problem

Every AI agent starts from zero.

No memory of past sessions. No context from other models.
Every conversation is a blank slate.

**Synapse Layer fixes that.**

---

## How It Works

```
Claude ───────┐
              │
Cursor ───────┼──→ Synapse Layer → governed recall → any agent
              │
ChatGPT ──────┘
```

Save once. Recall anywhere.
Encrypted memory. Per-operation random IV.

---

## Quick Install

Get your token first:
[forge.synapselayer.org](https://forge.synapselayer.org) → Dashboard → Connect

### Claude Desktop

Edit `~/Library/Application Support/Claude/claude_desktop_config.json`:

```json
{
  "mcpServers": {
    "synapse-layer": {
      "command": "npx",
      "args": [
        "mcp-remote",
        "https://forge.synapselayer.org/api/mcp",
        "--header",
        "x-connect-token: sk_connect_YOUR_TOKEN"
      ]
    }
  }
}
```

### Cursor

Edit `.cursor/mcp.json` in your project root:

```json
{
  "mcpServers": {
    "synapse-layer": {
      "command": "npx",
      "args": [
        "mcp-remote",
        "https://forge.synapselayer.org/api/mcp",
        "--header",
        "x-connect-token: sk_connect_YOUR_TOKEN"
      ]
    }
  }
}
```

### Windsurf

Edit `~/.codeium/windsurf/mcp_config.json`:

```json
{
  "mcpServers": {
    "synapse-layer": {
      "command": "npx",
      "args": [
        "mcp-remote",
        "https://forge.synapselayer.org/api/mcp",
        "--header",
        "x-connect-token: sk_connect_YOUR_TOKEN"
      ]
    }
  }
}
```

### Any MCP Client

```json
{
  "mcpServers": {
    "synapse-layer": {
      "command": "npx",
      "args": [
        "mcp-remote",
        "https://forge.synapselayer.org/api/mcp",
        "--header",
        "x-connect-token: sk_connect_YOUR_TOKEN"
      ]
    }
  }
}
```

Restart your client. Done.

---

## What Changes

| Without Synapse Layer | With Synapse Layer |
|---|---|
| Agent forgets every session | Persistent memory across sessions |
| Context locked to one model | Cross-agent memory |
| Plaintext exposure risk | AES-256-GCM encrypted at rest |
| Repeated context injection | Governed recall on demand |
| No memory reliability signal | Trust Quotient scoring |

---

## Python SDK

```bash
pip install synapse-layer
```

```python
from synapse_memory.client import Synapse

client = Synapse(token="sk_connect_YOUR_TOKEN")

client.remember("User prefers concise technical responses")

results = client.recall("user preferences")
for result in results:
    print(result)
```

---

## Trust & Security

- AES-256-GCM encryption at rest
- Per-operation random IV
- Trust Quotient memory scoring
- Header-first MCP auth
- Designed for LGPD/GDPR alignment
- Apache 2.0

---

## Troubleshooting

| Symptom | Cause | Fix |
|---|---|---|
| `401 Unauthorized` | Missing or invalid token | Verify your `sk_connect_` token at [forge.synapselayer.org](https://forge.synapselayer.org) → Dashboard → Connect |
| `ECONNREFUSED` | Client not using `mcp-remote` | Ensure config uses `npx mcp-remote` with `--header` |
| Empty recall results | No memories stored yet | Call `save_to_synapse` first, then recall |

---

## Production

- Live MCP endpoint: `forge.synapselayer.org`
- MCP tools: 5 active (`recall`, `save_to_synapse`, `process_text`, `search`, `health_check`)

---

## Related Projects

| Project | Description |
|---------|-------------|
| [synapse-layer](https://github.com/SynapseLayer/synapse-layer) | Core server — MCP endpoint, encryption engine, pgvector indexing |
| [synapse-sdk-python](https://github.com/SynapseLayer/synapse-sdk-python) | Python SDK — LangChain, CrewAI, and A2A protocol adapters |
| [synapse-layer-langgraph](https://github.com/SynapseLayer/synapse-layer-langgraph) | LangGraph checkpoint saver with encrypted state persistence |

---

## Links

- Website: [synapselayer.org](https://synapselayer.org)
- Forge (Dashboard): [forge.synapselayer.org](https://forge.synapselayer.org)
- PyPI: [pypi.org/project/synapse-layer](https://pypi.org/project/synapse-layer/)
- Core Repo: [github.com/SynapseLayer/synapse-layer](https://github.com/SynapseLayer/synapse-layer)
- MCP Endpoint: `https://forge.synapselayer.org/api/mcp`

Apache 2.0 © Synapse Layer
