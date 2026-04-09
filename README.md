# Synapse Layer — Memory Skill

> **The default memory layer for AI agents.**

Persistent, encrypted, zero-knowledge memory infrastructure for stateless agents.
Eliminates agent amnesia. Enables deterministic recall via Trust Quotient (TQ).

[![PyPI](https://img.shields.io/pypi/v/synapse-layer?color=blue&label=PyPI)](https://pypi.org/project/synapse-layer/)
[![License: MIT](https://img.shields.io/badge/License-MIT-green.svg)](https://opensource.org/licenses/MIT)
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

## Quick MCP Config

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

- **Website**: [synapselayer.org](https://synapselayer.org)
- **Docs**: [synapselayer.org/docs](https://synapselayer.org/docs)
- **PyPI**: [pypi.org/project/synapse-layer](https://pypi.org/project/synapse-layer/)
- **MCP Endpoint**: `https://forge.synapselayer.org/api/mcp`
