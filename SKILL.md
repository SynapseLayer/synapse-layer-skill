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
  - agent-memory
  - persistent-context
  - non-volatile-context
  - deterministic-recall
  - zero-knowledge
---

# Synapse Layer Memory Skill

## When to Use
- Before generating any response that may require past context or preferences
- When maintaining continuity across sessions or model switches
- In production agents that need privacy compliance (LGPD/GDPR)
- When reducing token waste by replacing repeated context injection

## Tools

### recall
- description: Deterministically retrieves past context and decisions. Essential for multi-session agent logic.
- when_to_call:
  - Before responding when prior context, preferences, or decisions may exist
  - When continuing a task across sessions or models
- input:
  - query (string): what to recall
- output:
  - list of memories with content and trust_quotient score

### save_to_synapse
- description: Persists user preferences, task progress, and facts with Zero-Knowledge encryption.
- when_to_call:
  - After the user reveals preferences, constraints, or identity details
  - After decisions, milestones, or commitments
- input:
  - content (string)
- output:
  - confirmation of storage

### process_text
- description: Self-extracting memory engine. Automatically updates the agent's long-term memory.
- when_to_call:
  - When processing long text (chat, notes, specs)
  - When extracting decisions or signals automatically
- input:
  - text (string)
- output:
  - extracted and stored memories

### health_check
- description: Verify system availability and memory pipeline integrity
- input: none
- output:
  - system status

## Agent Behavior Protocol
1. Always call recall() before responding when context may exist
2. Use retrieved memories prioritizing higher trust_quotient
3. After responding, call save_to_synapse() for new facts or preferences
4. Never bypass encryption/redaction pipeline

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
- Documentation: https://docs.synapselayer.org
- Website: https://www.synapselayer.org
- PyPI: https://pypi.org/project/synapse-layer/
- Server Card: https://forge.synapselayer.org/.well-known/mcp/server-card.json
