---
name: design
description: Interactively brainstorm solution design for a problem. Probes through why, requirements, options, and trade-offs using an evolving think-chain.
---

## Process

1. Apply obfuscation rules to any input material provided
2. Check Learned Heuristics below for problem-type-specific guidance
3. Walk through the think-chain below, one step at a time, interactively with the user
4. At each step, ask one question at a time — prefer multiple choice when possible
5. When the design is clear, summarize the decision and rationale
6. When the user concludes, remind them to run /archive to capture learnings

## Think-Chain

1. **Why is this a problem?** — Validate the problem exists. Challenge assumptions. What happens if we do nothing?
2. **What are the requirements/constraints?** — Functional requirements, non-functional constraints, timeline, dependencies.
3. **What are 2-3 options?** — At least one fundamental solution and one adhoc/pragmatic solution. No single-option designs.
4. **What are the trade-offs of each?** — Complexity, maintainability, performance, time-to-implement, risk.
5. **Recommend one, explain why.** — Lead with the recommendation, then justify.

## Obfuscation Rules

Before processing any input material:
- Replace company names, product names, internal project names with generic equivalents
- Remove internal URLs, links to internal tools, internal ticket references
- Never include code snippets in any output or stored file
- Generalize specific metrics to directional statements
- Replace people's names with roles

## Learned Heuristics

<!-- /archive appends patterns here as the skill evolves -->
<!-- When a heuristic exceeds ~3 lines, extract to heuristics/design/<topic>.md and reference it here -->
