---
name: synapse-layer
description: "Persistent memory skill for AI agents. Remembers preferences, brand voice and decisions with Trust Quotient scoring."
version: "2.3.7"
author: Ismael Marchi
tags: [memory, mcp, ai-agents, llm, typescript, cross-agent, state-continuity]
---

# Synapse Layer — Memory Skill

> RAG retrieves. Synapse remembers.

## What This Does

Synapse Layer is a persistent memory infrastructure for AI agents. It solves
the stateless-agent problem: agents forget decisions, preferences, and context
across sessions. With Synapse, any MCP-compatible agent can store and recall
memories — AES-256-GCM encrypted at rest, scored by Trust Quotient for
reliability, and scoped per-user with tenant isolation. One agent stores,
another recalls. Memory survives across sessions, models, and tools.

**Category**: OAuth for AI Memory — State Continuity Layer.

## Agent Rules

**MUST:**
- `store()` after each interaction that contains a decision, preference, or constraint worth persisting.
- `recall()` before responding when the user references prior context, preferences, or past work.
- Filter recall results by `tq >= 0.7` when high confidence is required.
- Include `agent` identifier on every `store()` call for cross-agent traceability.

**MUST NOT:**
- Store PII without explicit user consent.
- Assume a memory exists without calling `recall()` first.
- Expose raw memory content in logs or error messages.
- Store ephemeral or throwaway content (e.g., "ok", "thanks").

## Trust Quotient (TQ)

Trust Quotient is a per-memory confidence score ranging from 0.0 to 1.0.

- **What it measures**: Reliability of a memory based on content density,
  semantic alignment with recall queries, and noise level.
- **How to use**: Filter recall results by `tq >= 0.7` for high-confidence
  decisions. Use `tq >= 0.5` for general context. Memories below 0.3 may
  contain noise or low-relevance content.
- **Scoring**: TQ = f(density, alignment, noise). Weights are proprietary
  and dynamically calibrated.

## Multi-LLM Compatibility

Synapse Layer works with any MCP-compatible client:

- **Claude** (Desktop + API) — native MCP support
- **GPT-4 / GPT-4o** — via Synapse Proxy (OpenAI SDK compatible)
- **Gemini** — via MCP bridge
- **Llama / Mistral / local models** — via MCP stdio bridge
- **LangChain / CrewAI / AutoGen** — via Python SDK adapters

## Links

- **Forge**: [forge.synapselayer.org](https://forge.synapselayer.org)
- **Docs**: [forge.synapselayer.org/docs](https://forge.synapselayer.org/docs)
- **SDK (Python)**: [pypi.org/project/synapse-layer](https://pypi.org/project/synapse-layer/)
- **GitHub**: [github.com/SynapseLayer](https://github.com/SynapseLayer)
