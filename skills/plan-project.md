---
name: plan-project
description: Interactively brainstorm project planning. Covers deliverables, dependencies, parallelization, testing, and sequencing using an evolving think-chain.
---

## Process

1. Apply obfuscation rules to any input material provided
2. Check Learned Heuristics below for problem-type-specific guidance
3. Walk through the think-chain below, one step at a time, interactively with the user
4. At each step, ask one question at a time — prefer multiple choice when possible
5. When the plan is clear, summarize the sequencing and key milestones
6. When the user concludes, remind them to run /archive to capture learnings

## Think-Chain

1. **What are the deliverables?** — Concrete outputs. What does "done" look like?
2. **What are the internal dependencies?** — What must happen before what? What's coupled?
3. **How can we parallelize?** — What workstreams are independent? Who can work on what simultaneously?
4. **How can we test each part in isolation?** — Unit boundaries. What can be validated independently?
5. **What are the integration points?** — Where do independent workstreams come together? What are the risks at those seams?
6. **What's the sequencing?** — Given the above, what's the optimal order? What's on the critical path?

## Obfuscation Rules

Before processing any input material:
- Replace company names, product names, internal project names with generic equivalents
- Remove internal URLs, links to internal tools, internal ticket references
- Never include code snippets in any output or stored file
- Generalize specific metrics to directional statements
- Replace people's names with roles

## Learned Heuristics

<!-- /archive appends patterns here as the skill evolves -->
<!-- When a heuristic exceeds ~3 lines, extract to heuristics/plan-project/<topic>.md and reference it here -->
