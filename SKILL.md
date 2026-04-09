---
name: synapse-layer-memory
description: >
  Persistent, encrypted, zero-knowledge long-term memory for AI agents.
  Provides cross-session continuity and deterministic recall via Trust
  Quotient (TQ) scoring. Use when the agent needs to remember past context,
  user preferences, or decisions across sessions.
capabilities:
  - memory_persistence
  - context_recall
  - pii_redaction
  - mcp_integration
keywords:
  - memory
  - long-term memory
  - recall
  - persistent context
  - agent memory
  - context storage
  - remember user preferences
  - synapse
  - trust quotient
  - MCP memory
  - cross-session continuity
---

# Synapse Layer Memory Skill

## When to Use
- Before generating any response that may require past context or preferences
- When maintaining continuity across sessions or model switches
- In production agents that need privacy compliance (LGPD/GDPR)
- When reducing token waste by replacing repeated context injection

## Tools

### recall
- description: Retrieve past memories sorted by Trust Quotient (TQ)
- input:
  - query (string): what to recall
- output:
  - list of memories with content and trust_quotient score

### store
- description: Persist new facts, preferences, or decisions with automatic
  PII redaction and AES-256 encryption
- input:
  - content (string): information to persist
- output:
  - confirmation of storage

### process_text
- description: Automatically extract decisions, milestones, and important
  signals from text and store them
- input:
  - text (string): raw text to process
- output:
  - list of extracted and stored memories

### health_check
- description: Verify system availability and trust pipeline integrity
- input: none
- output:
  - system status and capabilities

## Agent Behavior Protocol

Follow this loop on every interaction:

1. Call recall(query) BEFORE generating a response if past context may exist
2. Use retrieved memories to inform reasoning — prefer results with higher TQ
3. After generating a response, call store(content) for new relevant facts
4. Never bypass the security pipeline — all data passes through PII redaction
   and encryption automatically

## Examples

```python
import asyncio
from synapse_layer import SynapseMemory

async def main():
    memory = SynapseMemory(agent_id="agent-001")

    # Store a fact
    await memory.store("User prefers concise technical responses")

    # Recall relevant context before responding
    results = await memory.recall("user communication preferences")
    for r in results:
        print(f"{r.content} (TQ: {r.trust_quotient:.3f})")

asyncio.run(main())
```

## Security Rules
- All data passes through PII redaction, intent validation, AES-256
  encryption and differential privacy automatically
- Never expose raw sensitive data
- agent_id is required for scoped memory isolation

## MCP Integration

```json
{
  "mcpServers": {
    "synapse-layer": {
      "url": "https://forge.synapselayer.org/api/mcp"
    }
  }
}
```

## Links
- Documentation: https://synapselayer.org/docs
- Website: https://synapselayer.org
- PyPI: https://pypi.org/project/synapse-layer/
