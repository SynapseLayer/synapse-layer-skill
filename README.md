![Version](https://img.shields.io/badge/version-2.3.0-blue)
![PyPI](https://img.shields.io/pypi/v/synapse-layer)
![Security](https://img.shields.io/badge/MCP%20Security-10.0%2F10-brightgreen)
![License](https://img.shields.io/badge/license-Apache%202.0-blue)
![Status](https://img.shields.io/badge/status-production-green)

# Synapse Layer — Memory for AI Agents

> **RAG retrieves. Synapse remembers.**

Persistent, encrypted, cross-agent memory for any AI agent.
Server never sees plaintext. Works in 30 seconds.

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
Encrypted memory. Server never sees plaintext.

---

## Quick Install

Get your token first:
[synapselayer.org](https://synapselayer.org) → Dashboard → Connect

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

Restart your client. Done.

## What Changes

| Without Synapse Layer | With Synapse Layer |
|---|---|
| Agent forgets every session | Persistent memory across sessions |
| Context locked to one model | Cross-agent memory |
| Plaintext exposure risk | Encrypted memory — server never sees plaintext |
| Repeated context injection | Governed recall on demand |
| No memory reliability signal | TRUTH QUOTIENT™ scoring |

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

## Trust & Security

- AES-256-GCM encryption
- Server never sees plaintext
- TRUTH QUOTIENT™ memory scoring
- Header-first MCP auth
- Designed for LGPD/GDPR alignment
- Apache 2.0

## Production

- Live MCP endpoint: forge.synapselayer.org
- Version: v2.3.0
- MCP tools: 9 active

## Links

- Website: [synapselayer.org](https://synapselayer.org)
- Docs: [docs.synapselayer.org](https://docs.synapselayer.org)
- PyPI: [pypi.org/project/synapse-layer](https://pypi.org/project/synapse-layer/)
- Core Repo: [github.com/SynapseLayer/synapse-layer](https://github.com/SynapseLayer/synapse-layer)

Synapse Layer is the State Continuity Layer for AI agents.
Built for production. Designed for LGPD/GDPR alignment. Apache 2.0.
