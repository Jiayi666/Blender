# Blender

A stateful, Claude Code skills-based personal knowledge tool that learns how you digest information and adapts over time. Inspired by the [LLM Wiki by Andrej Karpathy](https://gist.github.com/karpathy/442a6bf555914893e9891c11519de94f).

Everyone processes knowledge differently. Blender learns your preferences — what summary structure works for you, what questions you tend to ask, how you reason through problems — and evolves its approach through a conversation archive feedback loop.

## Skills

- `/spoon-feed` — Generate a 60-second structured summary of any input material (docs, papers, design specs) with interactive drill-down. The skill evolves what it includes based on your past patterns.
- `/design` — Interactively brainstorm solution design for a problem. Walks through a think-chain: why is this a problem, what are the requirements, what are the options, what are the trade-offs.
- `/plan-project` — Interactively plan a project. Covers deliverables, dependencies, parallelization, isolated testing, integration points, and sequencing.
- `/archive` — Run after any skill session to capture learnings. Sanitizes the conversation, stores it, and analyzes your interaction patterns to update the originating skill's heuristics.

## How It Learns

The stored state exists to improve the skills themselves, not to be a queryable knowledge base. When you `/archive` a session, the agent analyzes where you pushed back, what follow-ups you asked, and what structural changes you requested. Those patterns get written back into the skill files as learned heuristics, so next time the agent has a better chance of getting it right on the first pass.

## Privacy

All stored data is obfuscated at both ingest and archive boundaries. Company names, internal URLs, specific metrics, people's names, and code snippets are never written to the Blender file tree.
