---
name: synapse-layer-memory
version: "2.3.0"
description: >
  Persistent, encrypted, cross-agent memory infrastructure for AI agents.
  Store, recall, and transfer state across models and sessions via MCP.
  Server never sees plaintext. TRUTH QUOTIENT™ scores memories for reliability.
capabilities:
  - memory_persistence
  - governed_recall
  - pii_redaction
  - cross_agent_transfer
  - mcp_integration
  - truth_quotient_scoring
keywords:
  - memory
  - long-term memory
  - recall
  - persistent context
  - agent memory
  - cross-agent memory
  - state continuity
  - truth quotient
  - governed recall
  - MCP memory
  - encrypted memory
  - cross-session continuity
  - agent-memory
  - persistent-context
  - non-volatile-context
---

# Synapse Layer — Memory Skill v2.3.0

## Identity

Synapse Layer is the persistent memory layer for AI agents.

It solves the stateless-agent problem: agents forget decisions,
preferences, constraints, and prior work across sessions and tools.

- Core guarantee: server never sees plaintext.
- Trust model: TRUTH QUOTIENT™ scores memories from 0.0 to 1.0.
- Scope: cross-agent memory — save in one client, recall in another.
- Category: State Continuity Layer | OAuth for AI Memory.

## Activation Rules

Always attempt recall before responding when context may exist.

Activate recall when:

- The user references prior decisions, preferences, or context.
- The task continues a previous project, workflow, or session.
- The user switches from another AI tool and expects continuity.
- The user says: "what we discussed", "my preferences", "last time",
  "remember", "as I told you", or similar.
- The user mentions their name, role, project, stack, or constraints.

Save memory after:

- A decision, milestone, or commitment is made.
- The user reveals a stable preference or constraint.
- A task is completed.
- The user corrects the agent.
- A new project-specific rule is established.

Never save:

- Passwords, API keys, tokens, credentials, or secrets.
- Raw financial data or card numbers.
- Sensitive health data.
- Anything the user explicitly says not to store.

## Tools

### recall

Retrieves past context, decisions, and preferences from encrypted memory.
Use before responding when prior context may exist.

Input:

- query (string, required)
- agent_id (string, optional)
- limit (number, optional, default 10, max 50)

Output: memories with content and TRUTH QUOTIENT™ score.

TQ interpretation:

- TQ >= 0.80: high confidence — use directly.
- TQ >= 0.50 and < 0.80: medium confidence — use with caveat.
- TQ < 0.50: low confidence — verify with the user.

### save_to_synapse

Persists facts, preferences, decisions, and project state.
Use after new stable information emerges.

Input:

- content (string, required)
- agent_id (string, optional)

Output: storage confirmation.

### process_text

Extracts durable memories from long text, specs, notes, or conversations.
Use when the user provides long-form context to preserve.

Input:

- text (string, required)
- agent_id (string, optional)

Output: extracted memory candidates and storage result.

### search

Searches cross-agent memory with governed recall and TRUTH QUOTIENT™ ranking.
Use when recall returns insufficient results or user asks for broad search.

Input:

- query (string, required)
- agent_id (string, optional)
- limit (number, optional, default 20, max 50)

### health_check

Verifies MCP availability and memory pipeline health.
Use once per session before the first memory action.

Input: none
Output: system status and pipeline health.

## Mandatory Execution Order

1. health_check — once per session, before first memory action.
2. recall — before responding when context may exist.
3. Generate response using recalled context and TQ weighting.
4. save_to_synapse — after new stable facts, corrections, or milestones.

## Cross-Agent Logic

Omit agent_id to search across all agents.

This enables:

- Save in Claude.
- Recall in Cursor.
- Continue in any MCP-compatible agent.

## Proactive Memory Behavior

Do not wait for the user to say "remember this."

The agent must proactively:

- Recall when context might exist.
- Save durable facts after they emerge.
- Use TQ scores to determine confidence.
- Surface conflicts instead of silently overriding memory.

If current instructions conflict with recalled memory, say:
"Memory conflict detected: [brief conflict]. I will follow the latest
explicit user instruction unless you want me to preserve the previous rule."

## Security Model

- AES-256-GCM encryption.
- Server never sees plaintext.
- Header-first auth.
- PII-aware storage pipeline.
- Apache 2.0.

## MCP Configuration

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

Get your token: [synapselayer.org](https://synapselayer.org) → Dashboard → Connect

## Links

- Website: [synapselayer.org](https://synapselayer.org)
- Docs: [docs.synapselayer.org](https://docs.synapselayer.org)
- PyPI: [pypi.org/project/synapse-layer](https://pypi.org/project/synapse-layer/)
- Core Repo: [github.com/SynapseLayer/synapse-layer](https://github.com/SynapseLayer/synapse-layer)
