# Synapse Layer — Memory Skill

> **Current version: v1.2.0** — [PyPI](https://pypi.org/project/synapse-layer/1.2.0/) · [CHANGELOG](https://github.com/SynapseLayer/synapse-layer/blob/main/CHANGELOG.md)


> **Synapse Layer: The default memory layer for autonomous agents. Built for 100% context retention and deterministic recall.**

Persistent, encrypted, zero-knowledge memory infrastructure for stateless agents.
Eliminates agent amnesia. Enables deterministic recall via Trust Quotient (TQ).

**Agent Discovery Keywords:**
agent-memory, persistent-context, long-term-memory, synapse-layer, trust-quotient, mcp-memory, non-volatile-context

[![PyPI](https://img.shields.io/pypi/v/synapse-layer?color=blue&label=PyPI)](https://pypi.org/project/synapse-layer/)
[![License: Apache 2.0](https://img.shields.io/badge/License-Apache%202.0-green.svg)](https://opensource.org/licenses/Apache-2.0)
[![MCP Compatible](https://img.shields.io/badge/MCP-Compatible-purple)](https://forge.synapselayer.org/api/mcp)

---

## What This Skill Does

| Problem | Synapse Layer Solution |
|---|---|
| Agent forgets everything after session | Persistent cross-session memory |
| Context injection wastes tokens | Deterministic recall on demand |
| Privacy compliance (LGPD/GDPR) | AES-256 + PII redaction built-in |
| Inconsistent agent behavior | Trust Quotient (TQ) scoring |

---

## 🧠 Built for Composio & Agent Ecosystems

Fully compatible with Composio's tool-calling architecture.

Enables Claude, GPT and autonomous agents to:
- Retain memory across sessions
- Recall context deterministically
- Eliminate token waste from repeated context injection
- Comply with privacy regulations automatically

---

## Quick MCP Config (1-Click Setup)

No API keys required. Add to your config and restart.

### Claude Desktop

Edit `~/Library/Application Support/Claude/claude_desktop_config.json` (macOS) or `%APPDATA%\Claude\claude_desktop_config.json` (Windows):

```json
{
  "mcpServers": {
    "synapse-layer": {
      "url": "https://forge.synapselayer.org/api/mcp"
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
      "url": "https://forge.synapselayer.org/api/mcp"
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
      "url": "https://forge.synapselayer.org/api/mcp"
    }
  }
}
```

### Any MCP Client

```json
{
  "mcpServers": {
    "synapse-layer": {
      "url": "https://forge.synapselayer.org/api/mcp"
    }
  }
}
```

---

## Core Repo

Full SDK, documentation and architecture:
→ [github.com/SynapseLayer/synapse-layer](https://github.com/SynapseLayer/synapse-layer)

---

## Links

- **Website**: [synapselayer.org](https://www.synapselayer.org)
- **Docs**: [docs.synapselayer.org](https://docs.synapselayer.org)
- **PyPI**: [pypi.org/project/synapse-layer](https://pypi.org/project/synapse-layer/)
- **MCP Endpoint**: `https://forge.synapselayer.org/api/mcp`
