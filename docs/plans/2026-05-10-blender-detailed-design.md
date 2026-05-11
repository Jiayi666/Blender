# Blender Detailed Design

## Overview

Blender is a Claude Code skills-based personal knowledge tool that learns from conversations to improve how it presents and organizes information. It uses the local filesystem for state, with skill files that evolve through usage via an archive feedback loop.

The system is NOT a queryable knowledge base. Stored state exists to improve the skills themselves — how the agent presents, probes, and structures information — not to retrieve past knowledge.

## Architecture: Skill Files with Embedded Heuristics

Each skill is a Claude Code skill markdown file with two sections: static logic (process/think-chain) and learned heuristics (patterns appended by /archive). Skills evolve in-place. When a heuristic becomes complex enough (>3 lines), it gets extracted to a separate file under `skills/heuristics/<skill>/`.

## File Structure

```
Blender/
├── skills/
│   ├── spoon-feed.md
│   ├── design.md
│   ├── plan-project.md
│   ├── archive.md                 # Dispatcher with shared logic
│   ├── archive-spoon-feed.md
│   ├── archive-design.md
│   ├── archive-plan-project.md
│   └── heuristics/
│       ├── spoon-feed/
│       ├── design/
│       └── plan-project/
├── index/
│   ├── spoon-feed-index.md
│   ├── design-index.md
│   └── plan-project-index.md
├── raw/
│   ├── spoon-feed/
│   ├── design/
│   └── plan-project/
├── compact/
│   ├── spoon-feed/
│   ├── design/
│   └── plan-project/
├── docs/
├── ProductDesign.md
└── README.md
```

## Data Flow

```
index (categorized pointers) -> compact file (conversation analysis) -> raw file (full sanitized conversation)
```

The agent reads left-to-right: index to find relevant problem types, compact files for detail, raw only if needed.

## Index Files

Flat categorized lists of pointers to compact files. Categories represent problem types (trade-off analysis, system design concepts, process/methodology, etc.), not knowledge domains. Categories evolve as /archive creates or reclassifies them.

```markdown
# Spoon-Feed Index

## Trade-off Analysis
- [2026-05-10-raft-consensus](../compact/spoon-feed/2026-05-10-raft-consensus.md)

## System Design Concepts
- [2026-05-12-cap-theorem](../compact/spoon-feed/2026-05-12-cap-theorem.md)
```

## Compact Files

Short summaries (~20-30 lines) focused on conversation dynamics, not source material content.

```markdown
# 2026-05-10 — Trade-off Analysis (Consensus Paper)

## Problem Type
Trade-off analysis of a distributed systems concept

## Think-Chain Used
1. Led with mechanism overview
2. Key takeaways focused on practical implications
3. Drill-down into failure modes

## What Worked
- Structuring takeaways as "what this means for your systems"

## What Didn't
- Initial summary too theoretical — user wanted operational framing

## Heuristics Extracted
- "For trade-off analysis problems, lead with failure modes not happy path"

## Raw File
[link](../raw/spoon-feed/2026-05-10-raft-consensus.md)
```

## Skill File Structure

Each skill has frontmatter, static process, and a learned heuristics section that grows via /archive.

```markdown
---
name: <skill-name>
description: <one-line description>
---

## Process
<static think-chain>

## Obfuscation Rules
<sanitization rules>

## Learned Heuristics
<!-- /archive appends patterns here -->
<!-- When a heuristic exceeds ~3 lines, extract to heuristics/<skill>/<topic>.md -->
```

## Default Skill Think-Chains

### /spoon-feed
1. Identify the problem type (trade-off analysis, new concept, methodology, etc.)
2. Generate 60-second summary: one-line purpose, 3-5 key takeaways, "so what" implications
3. Present summary, offer drill-down
4. Answer follow-ups with further research as needed

### /design
1. Why is this a problem? (validate the problem exists)
2. What are the requirements/constraints?
3. What are 2-3 options? (fundamental vs. adhoc)
4. What are the trade-offs of each?
5. Recommend one, explain why

### /plan-project
1. What are the deliverables?
2. What are the internal dependencies?
3. How can we parallelize?
4. How can we test each part in isolation?
5. What are the integration points?
6. What's the sequencing?

### /archive (dispatcher)
1. Detect which skill was used in the session
2. Delegate to archive-<skill>.md
3. Sub-skill sanitizes, stores (raw + compact + index entry), and analyzes conversation
4. Updates the parent skill's Learned Heuristics section

## Archive Workflow

1. User invokes /archive after any skill session concludes.
2. archive.md (dispatcher) identifies which skill was used, delegates to archive-<skill>.md.
3. The sub-skill executes three steps:
   - **Sanitize**: strip sensitive data using obfuscation rules.
   - **Store**: write sanitized raw file to raw/<skill>/YYYY-MM-DD-<topic>.md, generate compact version in compact/<skill>/, add entry to index/<skill>-index.md.
   - **Learn**: analyze conversation for patterns — where did the user push back, what follow-ups came up, what changed from initial output. Update the skill file's Learned Heuristics (or create/update a heuristic sub-file).

The "Learn" step specifically looks for:
- Questions the user asked that the skill should have anticipated
- Structural changes the user requested
- Topic-specific preferences
- Patterns across previous archived sessions with similar problem types

## Obfuscation

Applied at two boundaries:

1. **On ingest**: when an external doc is provided to any skill, sanitize before processing. The agent works with the sanitized version throughout.
2. **On archive**: before writing any file to disk, another sanitization pass catches anything that leaked through conversation.

Rules:
- Company/product names -> generic equivalents ("CompanyX", "ServiceA")
- Internal URLs -> removed
- Specific metrics/numbers -> directional statements ("increased significantly")
- People's names -> roles ("the tech lead", "the reviewer")
- No code snippets ever written to the Blender file tree

## Scope

v1 includes all four skills. Priority is the /spoon-feed + /archive loop. /design and /plan-project ship with defaults and basic archiving but are expected to evolve more slowly.
