---
name: archive
description: Archive a completed skill session. Sanitizes, stores, and extracts learnings to improve the originating skill. Dispatches to per-skill archive sub-files.
---

## Process

1. Identify which skill was used in the current session (spoon-feed, design, or plan-project)
2. If the skill cannot be determined, ask the user
3. Delegate to the appropriate archive sub-skill:
   - spoon-feed -> see [archive-spoon-feed.md](archive-spoon-feed.md)
   - design -> see [archive-design.md](archive-design.md)
   - plan-project -> see [archive-plan-project.md](archive-plan-project.md)

## Shared Archive Logic

All archive sub-skills follow these three steps:

### Step 1: Sanitize

Apply obfuscation rules to the full conversation before writing anything to disk:
- Replace company names, product names, internal project names with generic equivalents
- Remove internal URLs, links to internal tools, internal ticket references
- Never include code snippets
- Generalize specific metrics to directional statements
- Replace people's names with roles

### Step 2: Store

1. Write the sanitized conversation to `raw/<skill>/YYYY-MM-DD-<topic>.md`
2. Generate a compact version in `compact/<skill>/YYYY-MM-DD-<topic>.md` focused on conversation dynamics (see Compact File Format below)
3. Add an entry to `index/<skill>-index.md` under the appropriate problem-type category (create a new category if none fits)

### Step 3: Learn

Analyze the conversation for skill improvement signals:
- Questions the user asked that the skill should have anticipated
- Structural changes the user requested (e.g., "put the trade-offs first")
- Topic/problem-type-specific preferences
- Compare with previous archived sessions of similar problem types (read index + compact files)
- Update the originating skill file's Learned Heuristics section
- If a heuristic exceeds ~3 lines, extract to `skills/heuristics/<skill>/<topic>.md`

## Compact File Format

```markdown
# YYYY-MM-DD — <Problem Type Category> (<Brief Topic>)

## Problem Type
<What type of thinking challenge this represents>

## Think-Chain Used
<Numbered steps the agent followed>

## What Worked
<Aspects of the summary/interaction the user responded well to>

## What Didn't
<Where the user pushed back, asked unexpected follow-ups, or restructured>

## Heuristics Extracted
<Specific patterns learned, quoted as actionable rules>

## Raw File
[link](../raw/<skill>/YYYY-MM-DD-<topic>.md)
```
