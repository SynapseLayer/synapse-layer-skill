---
name: synapse-layer
description: Persistent memory infrastructure for AI agents
version: "2.4.6"
author: Ismael Marchi
tags: [memory, mcp, ai-agents, llm, cross-agent]
---

# Synapse Layer — Memory Skill

## What This Does

Synapse Layer is persistent memory infrastructure for AI agents. It solves the
stateless-agent problem: agents forget decisions, preferences and context across
sessions. With Synapse, any MCP-compatible agent can store and recall memories —
AES-256-GCM encrypted at rest, scored by Trust Quotient for reliability, and
scoped per user, agent, project and tenant. One agent stores; another recalls.
Memory survives across sessions, models and tools.

## Agent Rules

**MUST:**
- Call `recall` before responding when the user references prior context, preferences or past work.
- Call `save_to_synapse` only when the user shares a durable decision, preference, constraint or fact, and the tenant policy allows it.
- Include `agent_id` on every save for cross-agent traceability.
- Respect memory scope (`agent` vs `tenant`) and project boundaries.
- Treat Trust Quotient as a heuristic, not a guarantee; thresholds are tenant-calibrated.

**MUST NOT:**
- Store PII without explicit user consent.
- Store secrets, credentials, tokens or ephemeral content (e.g. "ok", "thanks").
- Store third-party data without authorization.
- Save on every turn or auto-save entire conversations.
- Assume a memory exists without calling `recall` first.
- Expose raw memory content in logs or error messages.
- Claim zero-knowledge, end-to-end encryption or certified compliance.

## Write Policy

Durable, authorized, minimal, scoped:

1. **Durable** — decisions, preferences, constraints and facts worth recalling later.
2. **Authorized** — tenant policy wins; when in doubt, ask before storing.
3. **Minimal** — store the smallest useful fact, not the whole conversation.
4. **Scoped** — use the narrowest scope that still serves the user (`agent` by default; `tenant` only when the user asks for cross-agent memory).

If the policy denies a write, or consent is unclear, do not store.

## Tool Names

Use the real MCP tool names:

- `recall` (alias: `recall_memory`) — semantic/temporal/priority/hybrid retrieval. Requires a `reason`.
- `save_to_synapse` (aliases: `save_memory`, `store_memory`) — persist a memory.
- `search` — full-text lookup.
- `list_memories` — browse metadata without full content.
- `initialize_context` — preload context at session start.
- `memory_feedback` — adjust trust scoring with `used`, `ignored`, `helpful` or `irrelevant`.
- `neural_handover` — consume a one-time handover token.
- `health_check`, `process_text`, `slo_report` — operations and bulk extraction.

## Trust Quotient (TQ)

Trust Quotient is a per-memory confidence score from 0.0 to 1.0.

- **What it measures:** confidence, recency, usage and semantic alignment with the recall query.
- **How to use:** as a ranking heuristic. Thresholds are tenant-calibrated; `0.7` is not a universal guarantee of reliability.
- **Scoring:** weights are proprietary and dynamically calibrated.

## Multi-LLM Compatibility

Synapse Layer works with any MCP-compatible client:

- **Claude** (Desktop + API) — native MCP support
- **GPT / Gemini / local models** — via an MCP-compatible bridge
- **LangChain / CrewAI / AutoGen** — via Python SDK adapters (experimental where noted)

## Links

- **Forge:** [forge.synapselayer.org](https://forge.synapselayer.org)
- **Docs:** [forge.synapselayer.org/docs](https://forge.synapselayer.org/docs)
- **Claims & limits:** [FEATURES.md](https://github.com/SynapseLayer/synapse-layer/blob/main/FEATURES.md)
- **SDK (Python):** [pypi.org/project/synapse-layer](https://pypi.org/project/synapse-layer/)
- **GitHub:** [github.com/SynapseLayer](https://github.com/SynapseLayer)
