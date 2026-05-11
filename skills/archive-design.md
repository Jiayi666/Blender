---
name: archive-design
description: Archive logic specific to design sessions. Called by archive.md dispatcher.
---

## Process

This sub-skill is invoked by [archive.md](archive.md). Follow the shared archive logic (Sanitize, Store, Learn) with these design-specific additions:

### Sanitize

Follow shared obfuscation rules from archive.md. Additionally:
- Generalize architectural components to generic names (e.g., "a message queue" not the specific product)
- Preserve the structural patterns and trade-off reasoning — that's the valuable part

### Store

Follow shared store logic. When writing the compact file, pay special attention to:
- Which think-chain steps generated the most discussion
- Where the user challenged assumptions or redirected
- How the final recommendation compared to the initial framing

### Learn

When analyzing the conversation, focus on signals specific to design:
- **Think-chain ordering**: Did the user want to explore options before fully defining requirements? Did they skip steps?
- **Option depth**: Did the user want more or fewer options? More fundamental or more pragmatic?
- **Trade-off framing**: What dimensions mattered most to the user (complexity vs. time, risk vs. completeness)?
- **Challenge patterns**: Where did the user push back on the agent's reasoning?

Update `skills/design.md` Learned Heuristics with findings. Pattern format:
```
- For <problem type>: <specific guidance>
```
