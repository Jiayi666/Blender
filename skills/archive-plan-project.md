---
name: archive-plan-project
description: Archive logic specific to plan-project sessions. Called by archive.md dispatcher.
---

## Process

This sub-skill is invoked by [archive.md](archive.md). Follow the shared archive logic (Sanitize, Store, Learn) with these plan-project-specific additions:

### Sanitize

Follow shared obfuscation rules from archive.md. Additionally:
- Generalize team names and org structures
- Preserve dependency patterns and sequencing logic — that's the valuable part

### Store

Follow shared store logic. When writing the compact file, pay special attention to:
- How the user structured parallelization
- What testing isolation strategies were discussed
- Where integration risk was identified

### Learn

When analyzing the conversation, focus on signals specific to project planning:
- **Sequencing preferences**: Does the user prefer depth-first or breadth-first planning? Critical path focus or balanced workstreams?
- **Granularity**: Did the user want more or less detail in task breakdown?
- **Risk framing**: What types of risks did the user focus on (technical, timeline, integration, people)?
- **Parallelization patterns**: How aggressively does the user parallelize? What are their coupling thresholds?

Update `skills/plan-project.md` Learned Heuristics with findings. Pattern format:
```
- For <problem type>: <specific guidance>
```
